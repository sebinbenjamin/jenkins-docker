This docker image contains Jenkins CI, and has the ability to run docker on a host docker server from inside jenkins.
The latest tag pulls the weekly jenkins release and stable tag pulls the jenkins LTS release. Latest version of OpenJDK 8 JDK is used instead of JRE.

You may use ```-v $PWD:/var/jenkins``` to persist jenkins home, data.

```docker run -d -p 8080:8080  -v $PWD/data:/var/jenkins sebinbenjamin/jenkins```

  #### Using a host docker server
To use a host docker server, you just need to mount /var/run/docker.sock into the jenkins container. This allows jenkins to start docker containers in the same host docker engine which runs it.

```docker run -p 8080:8080 -v /var/run/docker.sock:/var/run/docker.sock sebinbenjamin/jenkins```

  #### Why I used OpenJDK JDK instead of JRE?

Well, for certain reason not excluding running gradle/maven builds from jenkins, I need to use JDK from jenkins. 

For example
```docker run -v $PWD/apache-maven-3.3.9:/opt/apache-maven-3.3.9  -v $PWD/gradle-3.4.1:/opt/gradle/gradle-3.4.1```

The above example assumes that maven & gradle are in the path with respect to $PWD.
