# sonar-clojure plugins
Uses eastwood and kibit to analyze clojure code
### Contributors
###### [Zobair Shahadat](https://github.com/zmsp/)
###### [Javier Hilty](https://github.com/hiltyj/)

### Sample Output
![alt tag](https://raw.githubusercontent.com/zmsp/sonar-clojure/master/sample-output.png)
### Prerequisites

##### For linux system
* Need to install [docker-sonar image](https://github.com/harbur/docker-sonarqube) and create a shared volume by adding the following onto the docker-compose.yml file under sonarqube. (See [example](https://github.com/zmsp/sonar-clojure/tree/master/Resources))

```  
volumes:
    - /opt/sonar/extensions:/opt/sonar/extensions
```
* Need to install [sonar-scanner] (https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner) and configure sonar-runner.properties to make sonar server accessible (See [example](https://github.com/zmsp/sonar-clojure/tree/master/Resources))

* Need to have [Eastwood](https://github.com/jonase/eastwood) and [Kibit](https://github.com/jonase/kibit) added to the profiles.clj (locaed on .lein/) file as plugins.

WARNING: If loading your code (particularly test files) causes side effects like writing files, opening connections to servers, modifying databases, etc., running this plugin on your code will do that too. 
##### For Windows
Wasn't tested on windows but plausible to run with little modification to source code. 

### 1. Get the plugin

#### Download the jar
[Download](https://github.com/zmsp/sonar-clojure/releases/)

#### Compiling from Source
* Clone this project
* CD to the project
* Run `mvn package`
* Find the resulting jar in the target folder

### 2. Placing the jar file 

Place the jar produced from above step onto `/opt/sonar/extensions/plugins`

### 3. Run 
Run docker-compose up from your [docker-sonar image](https://github.com/harbur/docker-sonarqube) folder

### 4. Using the plugin

* Create a sonar-project.properties file
    * Add the line `sonar.import_unknown_files=true` see the [example](https://github.com/zmsp/sonar-clojure/tree/master/Resources)
* [Run](https://docs.sonarqube.org/display/SONAR/Analyzing+Source+Code) sonar-scanner. Make sure to have sonar server is running beforehand. 
* Run `sonar-scanner` from project folder
* Open Sonar `localhost:9000` on the browser 
* Place Clojure widget to the dashboard
* Optional: Place Size Metrics widget and resize the dashboard

# Thanks
## I am actively monitoring this repo. If you would like to contribute, or submit an issue feel free to do so. 
