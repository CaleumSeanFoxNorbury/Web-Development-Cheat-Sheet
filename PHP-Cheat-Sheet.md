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
