## Docker compose example

After downloading docker-sonar image edit the docker-compose.yml file to have shared extentions directory
```
postgresql:
  image: orchardup/postgresql:latest
  environment:
    - POSTGRESQL_USER=sonar
    - POSTGRESQL_PASS=xaexohquaetiesoo
    - POSTGRESQL_DB=sonar
  volumes:
    - /opt/db/sonarqube/:/var/lib/postgresql
  ports:
    - "5432:5432"
sonarqube:
  image: harbur/sonarqube:latest
  links:
    - postgresql:db
  environment:
    - DB_USER=sonar
    - DB_PASS=xaexohquaetiesoo
    - DB_NAME=sonar
  volumes:
    - /opt/sonar/extensions:/opt/sonar/extensions
  ports:
    - "9000:9000"
    - "443"
```

## sonar-project-properties
Need to have sonar.import_unknown_files=true in order to import clj and cljs files


Create a file called sonar-project.properties in the root directory of the clojure project.

```
#Required metadata

#Add an unique key
sonar.projectKey=MyClojureProjectKey

#Can be whatever
sonar.projectName=My Clojure Project Name
sonar.projectVersion=1.0

#Comma-separated paths to directories with sources (required)
sonar.sources=src/ , test/

#Must have this in order to import clj and cljs files form the sources
sonar.import_unknown_files=true

#Encoding of the source files
sonar.sourceEncoding=UTF-8
```

## sonar-runner configuration sonar-runner.properties
Localed in sonar-runner directory. Credentials are specific to harbor/docker-sonarqube

```
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonar

sonar.jdbc.username=sonar
sonar.jdbc.password=xaexohquaetiesoo

```

## Leiningen profiles.clj 
 located on home/.lein/profiles.clj
 Include eastwood and kibit in plugins
```
{
    :user {
        :plugins [
            [jonase/eastwood "0.2.1"]
            [lein-kibit "0.1.5"]
        ]
    }
}

```