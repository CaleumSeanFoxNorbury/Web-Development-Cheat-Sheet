# PHP

## Converting file to PDF

Files with variables (e.g., docx, doc, text) are converted by running through a collection of variables and using PHPWord template processor to set the value (this is done by using zip archive to run through the directories and changing values within `word/document.xml` where the document content is stored). Once the variables have been converted, we save the file within a temp folder.
After the variable conversion process has finished, we then need to convert the new temp file to pdf for outputting. This is done by using PHPWord and setting its PDF renderer using TCPDF PHP extension:

```
// Set the PDF renderer
Settings::setPdfRendererName('TCPDF');
Settings::setPdfRendererPath(ASSETS_PHP_ROOT.'tecnickcom/tcpdf/');
```

After this, we are able to create a PDF writer are able to save as a new temp file. After this process we delete the converted temp file mentioned above as this is now longer needed. Once the PDF temp file has been saved, we echo out the full directory path to the downloads file in which outputs our file content and then deletes the temp PDF file. 

```
            try{
                // Set the PDF renderer
                \PhpOffice\PhpWord\Settings::setPdfRendererName('TCPDF');
                \PhpOffice\PhpWord\Settings::setPdfRendererPath(ASSETS_PHP_ROOT.'tecnickcom/tcpdf/');

                // Load the document
                $phpWord = IOFactory::load($fullFilePath);

                $updatedFilePath = getATempLocation($fileName, $filePath, $useFullPath);                

                $pdfWriter = \PhpOffice\PhpWord\IOFactory::createWriter($phpWord, 'PDF');

                $pdfWriter->save($updatedFilePath.'.pdf');                 

                if(!file_exists($updatedFilePath.'.pdf')){
                    throw new Exception('Failed creating PDF');
                }
            } catch(Exception $e){
                throw new Exception('Unsupported file type');
            }
```

## Speeding Up Endpoints 

Requests can be heavy duty specially around database queries and loops, but these can be simplified in many ways so our requests dont take as long to process as we can achieve high speed performance.

```
                    // improved request by at least a second
                    $workTimesheetList = $oWorkTimesheet->getShiftsByDateRange($startDate, $endDate, "AND e.employeeTypeID = 1 AND e.depotID = ".$dbDepot['depotID']);

                    if($workTimesheetList){
                        $gatheredDates = [];
                        foreach($workTimesheetList as $dbWorkTimesheet) {
                            $sql_date = $dbWorkTimesheet['mysql_startDate'];
                            if(!in_array($gatheredDates, $sql_date)){
                                $valuesByDate = array_filter($workTimesheetList, function ($array) use ($sql_date) {
                                    return $array['mysql_startDate'] === $sql_date;
                                });

                                $clockTimesList = $oAppClockIn->getAll("AND ac.employeeID IN (".implode(", ", array_column($valuesByDate, 'employeeID')).") AND DATE_FORMAT(ac.startDateTime, '%Y-%m-%d' ) BETWEEN '".min(array_column($valuesByDate, 'mysql_startDate'))."' AND '".max(array_column($valuesByDate, 'mysql_endDate'))."'");
                                $clockinTotal = ($clockTimesList) ? count($clockTimesList) : 0;

                                $percentage = round(($clockinTotal / count(array_unique(array_filter(array_column($valuesByDate, 'employeeID'))))) * 100, 2);
                                $gatheredDates = array_column($valuesByDate, 'mysql_startDate');
                            }
                        }
                    }

                    // slow requests: embedded loops and query calls

                    $dateArray = getMonthsInRange($startDate, $endDate);
                    $percentages = [];
                    foreach($dateArray as $date) {
                        $workTimesheetList = $oWorkTimesheet->getShiftsByDate($date, "AND e.employeeTypeID = 1 AND e.depotID = ".$dbDepot['depotID'], true);

                        if($workTimesheetList){
                            $totalClockIns = 0;
                            $totalEmployees = count(array_unique(array_filter(array_column($workTimesheetList, 'employeeID'))));
                            $completedIDList = array();
                            foreach($workTimesheetList as $dbWorkTimesheet) {
                                if(!in_array($dbWorkTimesheet['employeeID'], $completedIDList)){
                                    $clockTimesList = $oAppClockIn->getAll("AND ac.employeeID = ".$dbWorkTimesheet['employeeID']." AND DATE_FORMAT(ac.startDateTime, '%Y-%m-%d' ) = '".$dbWorkTimesheet['mysql_startDate']."'");
                                    if($clockTimesList){
                                        $totalClockIns++;
                                    }
                                    $completedIDList[] = $dbWorkTimesheet['employeeID'];
                                }
                            }
                           $percentage = round(($totalClockIns / $totalEmployees) * 100, 2);

                           $percentages[] = $percentage;
                        } else {
                            $depotData[] = [
                                "depotName" => $dbDepot['name'],
                                "date" => $date,
                                "percentage" => "No Data"
                            ];
                        }
                    }
```
