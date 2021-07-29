# Bash Cheatsheet

## Commands
| Command | Purpose |
| ------- | ------- |
| pwd     | Prints current directory |
| ls -la  | Lists all files in current directory|
| touch \<filename> | Creates file with name 'filename' |
| mkdir \<foldername> | Creates folder with name 'foldername' | 
| cd \<foldername> | Change current directory to 'foldername' |
| cd .. | Change current directory to parent directory |
| cd ~ | Change current directory to home directory |
| cat \<filename> | Print contents of filename to console |
| rm -rf \<foldername> | Remove folder and it's contents |
| mv currentfile newlocation | move file |
| cp currentfile newlocation | copy file |
| sudo kill -9 $(sudo lsof -t -i:3000) | kill a port |