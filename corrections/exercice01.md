# Exercice01

1. `docker --help`
2. réponses:
   - `docker pull alpine:latest`
   - `docker run -it --name exercice01 alpine`
3. réponses:
   - `apk update`
   - `apk add git`
   - `mkdir app`
   - `cd ./app`
   - `git clone https://github.com/octocat/Hello-World`
   - `cd ./Hello-World`
4. réponses:
   - `vi README`
5. réponses:
   - `docker cp exercice01:/app/Hello-World/README ./README.md`
