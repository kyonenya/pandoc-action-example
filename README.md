> On Unix-like shells (like bash, for which your script is written) glob expansion (e.g. turning *.md into file1.md file2.md file3.md) is performed by the shell, not the application you're running. Your application sees the final list of files, not the wildcard.
https://stackoverflow.com/questions/49978926/concatenate-multiple-markdown-files-using-pandoc-on-windows
