# Домашнее задание к занятию 9 «Процессы CI/CD»

## Знакомство с SonarQube

Создал проект netology-hw, скачал sonar-scanner, запустил анализ кода - найдено 2 ошибки, 1 предупреждение.

Исправил найденные проблемы, запустил анализ кода повторно - ошибок не обнаружено, QG пройдены успешно.

Скриншот успешного прохождения анализа:

![sonar01.png](images%2Fsonar01.png)

## Знакомство с Nexus

Загрузил артефакты с необходимыми параметрами

![nexus01.png](images%2Fnexus01.png)

Файл `maven-metadata.xml` для артефакта имеет вид:
```
<?xml version="1.0" encoding="UTF-8"?>
<metadata modelVersion="1.1.0">
  <groupId>netology</groupId>
  <artifactId>java</artifactId>
  <versioning>
    <latest>8_282</latest>
    <release>8_282</release>
    <versions>
      <version>8_102</version>
      <version>8_282</version>
    </versions>
    <lastUpdated>20230603141107</lastUpdated>
  </versioning>
</metadata>
```

### Знакомство с Maven

Скачал maven, поменял в `pom.xml` блок с зависимостями под загруженный артефакт, запустил команду `mvn package`.

Артефакт успешно скачался:
```
(venv) alex@example ~/repo/netology-ci/ci03/mvn (master) $ ls ~/.m2/repository/netology/java/8_282/
java-8_282-distrib.tar.gz  java-8_282-distrib.tar.gz.sha1  java-8_282.pom.lastUpdated  _remote.repositories
```

Содержимое исправленного `pom.xml`:
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <groupId>com.netology.app</groupId>
  <artifactId>simple-app</artifactId>
  <version>1.0-SNAPSHOT</version>
   <repositories>
    <repository>
      <id>my-repo</id>
      <name>maven-public</name>
      <url>http://51.250.100.115:8081/repository/maven-public/</url>
    </repository>
  </repositories>
  <dependencies>
 <dependency>
      <groupId>netology</groupId>
      <artifactId>java</artifactId>
      <version>8_282</version>
      <classifier>distrib</classifier>
      <type>tar.gz</type>
    </dependency>
  </dependencies>
</project>
```
