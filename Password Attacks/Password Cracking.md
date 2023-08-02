GPU have higher hash rate than CPU, GPU are not available in kali VM

#### Mutating Wordlists

Hashcat

echo $1 $2 $3  c $! >> demo.rule
hashcat.exe -r demo.rule --stdout demo.txt
hashcat -m 0 crackme.txt rockyou.txt -r demo.rule --force