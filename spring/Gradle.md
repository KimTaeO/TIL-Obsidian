build.gradle 파일은 그 자체로 Project 객체이며, Project 인터페이스를 구현하는 구현체이다.

Project 객체는 Project 작업 단위에서 필요한 모든 작업들을 수행하기 위해 프로퍼티와 메서드들을 모아 놓은 슈퍼 객체이기도 하다.

대표적인 메서드로는 plugins, repositories, dependencies, application 등이 있다. 이 메서드들은 인자로 클로저를 넘겨줄 수 있어 다음과 같은 방식으로 정의될 수 있다
```
plugins {

}

repositories {

}

dependencies {

}

application {

}
```

해당 메서드들은 프로젝트가 빌드될 때 해당 메서드를 수행하는 task에 의해 수행된다

커스텀 메서드를 정의하는 방법으로는
```
ext.[커스텀 메서드] {

}
```
와 같은 형식으로 closure를 활용할 수 있다

### Project Property 정의
Project 객체를 위해 property를 정의할 수 있다
	 아무곳에나 ```project.[프로퍼티명] = 값``` 의 형식으로 작성한다

커스텀 프로퍼티를 정의하기 위해서는 커스텀 메서드를 정의하는 방법과 같이
```
project.ext.[커스텀 프로퍼티명] = 값
```
와 같은 형식으로 작성한다. 커스텀 프로퍼티에 접근하기 위해서는
```
project.[커스텀 프로퍼티명]
```
로 접근하면 된다