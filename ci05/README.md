# Домашнее задание к занятию 11 «Teamcity»


## Подготовка к выполнению

Подготовил инфраструктуру: `teamcity-server`, `teamcity-agent`, `nexus`.
Выполнил первоначальную настройку, авторизовал агент.
Форкнул репозиторий.

## Основная часть

Создал проект netology, подключил форк репозитория, настроил шаги для сборки, загрузил конфигурацию settings.xml.

![01-build steps.png](images%2F01-build-steps.png)

Указал в pom.xml ссылку на nexus, запустил сборку - всё прошло успешно, артефакт появился в nexus.

![02-build.png](images%2F02-build.png)
![03-nexus.png](images%2F03-nexus.png)

Настроил передачу `build configuration` в репозиторий.

![04-git-settings.png](images%2F04-git-settings.png)
![05-git.png](images%2F05-git.png)

Создал ветку `feature/add_reply` в репозитории:
```bash
git branch feature/add_reply
git checkout feature/add_reply
```
Добавил метод `sayForbidden` для класса `Welcomer`:

```java
public String sayForbidden(){
        return "Go away, hunter! Hunting is forbidden here";
}
```
Дополнил тест `welcomerSaysHunter` для нового метода:
```java
public void welcomerSaysHunter() {
        assertThat(welcomer.sayWelcome(), containsString("hunter"));
        assertThat(welcomer.sayFarewell(), containsString("hunter"));
        assertThat(welcomer.sayForbidden(), containsString("hunter"));
}
```
Запушил изменения, убедился, что тесты прошли успешно:

![06-test.png](images%2F06-test.png)

Вмержил изменения в мастер:
```bash
git checkout master
git merge feature/add_reply
```

Убедился, что нет собранного артефакта в сборке по ветке `master`. Настроил конфигурацию так, чтобы она собирала `.jar` в артефакты сборки:

![07-artifacts.png](images%2F07-artifacts.png)

Повторно собрал мастер: сборка прошла успешно, артефакты собраны.

![08-nexus2.png](images%2F08-nexus2.png)


Ссылка на репозиторий: https://github.com/AlexDrEamer42/example-teamcity



