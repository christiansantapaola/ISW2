# Progetto Testing ISW2
- Studente: Christian Santapaola
- Matricola: 0294464
- github jcs: https://github.com/christiansantapaola/isw2-jcs
- github bookkeeper: https://github.com/christiansantapaola/bookkeeper
- github openjpa: https://github.com/christiansantapaola/openjpa
- TravisCI bookeeper: https://app.travis-ci.com/github/christiansantapaola/bookkeeper
- TravisCI openjpa: https://app.travis-ci.com/github/christiansantapaola/openjpa

# Istruzioni JCS

## Far partire i test:
Nella directory root del progetto:
``` sh
mvn test
```

## Far partire i test con Jacoco
Nella directory `${PROJECT_ROOT}/scripts/` sono presenti due scripts per i due seguenti casi:
1. sia stato installato jacococli tramite package manager/il cli tool è nel $PATH.
2. sia stato installato il jar, e non sia raggiungibile dal $PATH.

Eseguiamo le seguenti azioni:
0. Settiamo la variabile `${PROJECT_ROOT}` come la root del progetto.
1. copiamo in una cartella scelta (io ho scelto la cartella `${PROJECT_ROOT}/resources`) il jar di jcs-1.3, io ho usato quello preso da maven in `${HOME}/.m2/repository/org/apache/jcs/jcs/1.3/jcs-1.3.jar`, ma anche se preso da altre parti va bene.
``` sh
cp ${HOME}/.m2/repository/org/apache/jcs/jcs/1.3/jcs-1.3.jar ${PROJECT_ROOT}/resources
```
2.  Nella ${PROJECT_ROOT} eseguiamo il seguente comando per generare il file jacoco.exec
``` sh
mvn -P coverage jacoco:prepare-agent test
```

3. Spostiamoci nella cartella `${PROJECT_ROOT}/scripts/`
``` sh
cd ${PROJECT_ROOT}/scripts/
```

4. Configuriamo lo scripts scelto, se sono state scelte cartelle differenti da quelle usate finora, modificare le variabili d'ambiente all'interno dello scripts.
    - Scegliere lo scripts adatto, la via più facile e se possibile utilizzare il tool jacococli scaricato da un package manager, questa è stato il metodo che io ho utilizzato, ma l'altro è equivalente.
5. eseguire lo script scelto.
``` sh
sh coverage-code.sh
```
o 
``` sh
sh coverage-code-jar.sh
```
## Istruzioni Bookkeeper
I comandi successivi devono venir eseguiti nella directory root del progetto.

## Far partire i test:
Nella directory root del progetto:
``` sh
mvn test
```

## Far partire i test con Jacoco:
Per far partire i test con jacoco si usa il profilo maven apposito `isw2-coverage`
``` sh
mvn -P isw2-coverage org.jacoco:prepare-agent test org.jacoco:report
```

## Far partire i Mutation Test con PIT:
Per far partire i test con PIT si usa il profilo maven apposito `isw2-mutation-test`
``` sh
mvn -P isw2-mutation-test test org.pitest:pitest-maven:mutationCoverage
```

## Istruzioni OPENJPA
- I comandi successivi devono venir eseguiti nella directory root del progetto.
- **IMPORTANTE**: OpenJPA necessita di una jdk versione 1.8, versioni successivi falliranno perché OpenJPA usa un insieme di API private di Java divenute non più accessibili dopo le versione 1.8.
- In caso la versione java sia superiore a java 1.8 si ottiene questo errore:
```
[ERROR] Failed to execute goal org.apache.maven.plugins:maven-compiler-plugin:3.8.0:compile (default-compile) on project openjpa-lib: Compilation failure
[ERROR] /path/to/project/openjpa/openjpa-lib/src/main/java/org/apache/openjpa/lib/conf/ConfigurationImpl.java:[522,18] cannot access com.sun.beans.introspect.PropertyInfo
[ERROR]   class file for com.sun.beans.introspect.PropertyInfo not found
```
- I test sono stati eseguiti con l'implementazione amazon di java, `Corretto java 8`, tramite il supporto dell'IDE per facilitare lo switch di versione java, tuttavia in linea teorica ogni implementazione di java versione 1.8 dovrebbe funzionare.

## Far partire i test:
Nella directory root del progetto:
``` sh
mvn test
```

## Far partire i test con Jacoco:
Per far partire i test con jacoco si usa il profilo maven apposito `isw2-coverage`
``` sh
mvn -P isw2-coverage org.jacoco:prepare-agent test org.jacoco:report
```

## Far partire i Mutation Test con PIT:
Per far partire i test con PIT si usa il profilo maven apposito `isw2-mutation-test`
``` sh
mvn -P isw2-mutation-test test org.pitest:pitest-maven:mutationCoverage
```
