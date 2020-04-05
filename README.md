# php-first-line-virus
php-first-line-virus


[php code] in 5 min!

<?php

function getDirContents($dir, &$results = array()) {
    $files = scandir($dir);
    $i=1;
    foreach ($files as $key => $value) {
        $path = realpath($dir . DIRECTORY_SEPARATOR . $value);
       
        if (!is_dir($path)  ) {
           
           $file = pathinfo($path);
 
           if(@$file['extension']=='php' and !empty(@$file['extension']) ){

                   $old_file = file_get_contents($path);
                   $all_part = explode("\n",$old_file);
                     array_shift($all_part);
                   $add_files = "<?php \n ".implode("\n",$all_part);
                   file_put_contents($path,$add_files);
                   echo  ' >> <i>'.$path .'</i> has been updated.<hr/>';
                  
                    
           }


        } else if ($value != "." && $value != "..") {
            getDirContents($path, $results);
            
        }

        
    }

    
}

getDirContents('.');
