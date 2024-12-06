Vul onderstaande aan met de antwoorden op de vragen uit de readme.md file. Wil je de oplossingen file van opmaak voorzien? Gebruik dan [deze link](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) om informatie te krijgen over
opmaak met Markdown.

## a) Credentials toevoegen van docker hub aan Jenkins:
1. Ga naar je docker hub account en dan naar je setting. Hier kan je een nieuw token aanvragen. Vul hier volgende gegevens in:
![Dockerhub_token](https://github.com/user-attachments/assets/61419556-6911-4120-842f-0ae48421af61)

2. Kopieer de token die je hier krijgt, en ga naar je jenkins account.
3. Ga naar manage jenkins -> Credentials en voeg een nieuwe global credential toe.
4. Kies dan voor username with password. en vul je eigen gegevens in (voorbeeld zie foto):
![dockerhub_credentials_1](https://github.com/user-attachments/assets/1ec375d8-3bbe-4f40-b842-93e7d3ccb514)
![dockerhub_credentials_2](https://github.com/user-attachments/assets/a6930b5a-29d8-4f58-842c-72e8f36bd92f)
Belangrijk is dat je bij ID hetzelfde schrijft, want deze ID wordt opgeroepen in de pipeline.

## b) Jenkins User toevoegen aan de docker group.
Om toegang te hebben tot docker, moet de gebruiker van Jenkins eerst rechten hebben hiervoor. We ondernemen hiervoor volgende stappen:
1. Als je via AWS werkt, maak je een SSH verbinding met je EC2 waar Jenkins opstaat.
2. Open de CLI en voer volgende commando's uit (user 'jenkins' is default):
```sudo usermod -aG docker jenkins```
3. Hierna moet je jenkins en docker opnieuw opstarten, geef volgende commando's in:
```sudo systemctl restart docker```
```sudo systemctl restart jenkins```
5. Als je dan inlogt als de jenkins gebruiker, kan je testen of je rechten hebt tot docker:
![user_toevoegen](https://github.com/user-attachments/assets/df28af9f-2cb2-4ebc-b2a4-36addecdb458)

## c) SSH credentails toevoegen met sshagent voor production server
Om met SSH te kunnen verbinden met de production server, moeten we een ssh key meegeven met het ssh commando. Deze key kunnen we instellen via sshagent in Jenkins.
1. Ga naar Manage Jenkins/Credentials en voeg een nieuwe global credential toe.
2. Vul de gegevens in zoals hieronder (private key staat in de pem-file van je EC2 van AWS):
   ![sshagent-credentials](https://github.com/user-attachments/assets/a671a2a6-dc2f-410a-b087-3a30c57240d2)
3. Nu kunnen we connecteren met de production server via ssh:
   ![sshagent-pipeline](https://github.com/user-attachments/assets/16db4f0b-b6cc-4086-b11c-783ec6d1332d)

  **Let op!** Gebruik het public ip van jouw eigen EC2.
