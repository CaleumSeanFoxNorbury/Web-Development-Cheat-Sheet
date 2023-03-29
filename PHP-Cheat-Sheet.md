# PHP

Converting file to pdf

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
