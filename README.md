# Lian-Lu-Write-up
Lian Lu by tryhackme

So today we gonna do tryhackme Lian_lu first thing first we need to aquired the ip for lian lu in tryhackme

<img width="1311" height="169" alt="image" src="https://github.com/user-attachments/assets/a0fdaa36-8af1-4e71-a138-b3d738a1706e" />


TARGET : 10.49.154.242

As usual we goin to use nmap -sC -sV -Pn <Target ip > 

<img width="774" height="562" alt="image" src="https://github.com/user-attachments/assets/953be813-0220-4328-81db-937ed36b4278" />

so we can see alot of port open such as 21,22,80 and 111 so based on nmap scan we see there is no code 230 for ftp but its fine we gonna try check out any info on port 80

<img width="866" height="764" alt="image" src="https://github.com/user-attachments/assets/d287faee-45f5-4cce-9c3a-b17bf8658680" />


nothing useful info just normal website so next we goin to try find it hidden directory using dirbuster

SCRIPT: gobuster dir -u http://10.49.154.242 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 

<img width="770" height="337" alt="image" src="https://github.com/user-attachments/assets/21d718da-766f-40b5-8bec-91ea90934ab2" />

so we find island directory lets check it out, who knows maybe epstein files in there...jk

<img width="865" height="761" alt="image" src="https://github.com/user-attachments/assets/70a45c8b-bc76-43b9-8944-460c2be8581c" />


<img width="866" height="758" alt="image" src="https://github.com/user-attachments/assets/c6e53dc8-3d63-4b58-bf84-19f2cb46a717" />

it said code is vigilante probaly it's username


SCRIPT: gobuster dir -u http://10.49.154.242/island -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 

we do found something 
<img width="771" height="315" alt="image" src="https://github.com/user-attachments/assets/0f25d9d8-eb2d-440e-ae56-7bcacedcf18c" />

lets check it out

<img width="861" height="762" alt="image" src="https://github.com/user-attachments/assets/efcf3e39-8a73-4190-b7ad-ed15d8d7af3b" />


<img width="858" height="754" alt="image" src="https://github.com/user-attachments/assets/5412eac0-e341-4095-86ed-3f42ae754efa" />

hidden message just like before "you can avail your .ticket here but now?"
seems like .ticket is extension we goin to try this command


SCRIPT: gobuster dir -u http://10.49.154.242/island/2100 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .ticket -t 50

<img width="765" height="333" alt="image" src="https://github.com/user-attachments/assets/d6e84bba-89ee-4193-ba0c-96fe1ba30be7" />


so we found new directory green_arrow.ticket we go check it out


<img width="861" height="249" alt="image" src="https://github.com/user-attachments/assets/56394c36-96d2-48ec-85c8-e6dd694425c8" />

hidden message meaning something but what it is?

we going to use decode using this command 

SCRIPT:
python3 - <<'PY'
import base58
print(base58.b58decode("RTy8yhBQdscX").decode())
PY

<img width="527" height="111" alt="image" src="https://github.com/user-attachments/assets/4797d193-9c1a-4769-a7c9-c74dca3c21ce" />


so we found password and the username now let go to ftp port

<img width="345" height="188" alt="image" src="https://github.com/user-attachments/assets/18e6d986-3cda-46bc-9684-3ad3328d37d2" />

so we did get into ftp using the password and username

<img width="776" height="626" alt="image" src="https://github.com/user-attachments/assets/6392ab25-cbaf-4503-9e24-2a239bd1cc27" />

first try ls then get all the file inside

after that ls -la to see all files

<img width="629" height="250" alt="image" src="https://github.com/user-attachments/assets/d567afcb-f259-4138-956a-b133c43ed395" />

get all the files inside


i cat other_user file i can see few username but not sure it usable or not such as slade wilson 

<img width="766" height="403" alt="image" src="https://github.com/user-attachments/assets/09a1d769-5913-4ba3-8496-d621cb906a2a" />

now i try to open the image in the ftp using steghide

<img width="685" height="275" alt="image" src="https://github.com/user-attachments/assets/ae711462-cff0-42a0-99a9-6c90640227b4" />

Leave_me_alone.png → Unsupported format error
Queen's_Gambit.png → Unsupported format error
aa.jpg → Requires a passphrase

so some of them not in correct format and 1 of them are encrypted


