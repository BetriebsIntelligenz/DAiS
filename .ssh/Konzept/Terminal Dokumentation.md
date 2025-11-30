# Terminal Live Mitschnitt
script --timing=time.log --flush --append terminal.log

# Terminal Mitschnitt beenden
exit

# Terminal Lesbar machen
cat terminal.log   | sed -r 's/\x1B\[[0-9;]*[A-Za-z]//g'   | col -b   > terminal-clean.txt 