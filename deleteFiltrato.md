ls -la|awk ' {if($5==0)  print $9 }'|xargs rm 
