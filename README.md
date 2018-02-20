Gradle

1. Look up java plugin documentation. Make changes in manifest to make it executable with correct class. When run using java -jar JAR_NAME_HERE the output should be text "Hello World" on the console. For creating a jar file add the below source code in build.gradle and then build project.

jar {
      manifest {
          attributes(
  
                  'Main-Class': '<path>'
  
          )
      }
 }

2. look up idea plugin. make changes in build.gradle so that the sources of src/main/java as well as src/main/java2 are taken as sources. Ensure that when you make JAR file class files in both are added to the JAR. This will teach you how projects with non-conventional structure can be used with gradle. For adding directory as source add below code.

sourceSets {
    main {
        java {
            srcDirs = ['src/main/java', 'src/main/java2']
        }
        
    }
}

3. add 2 files file1.xml and file1.txt in src/main/resources manually. make changes so that when creating jar only file1.xml is added to the jar.  For excluding directory/file add below code.

sourceSets {
    main {
        resources{
            srcDirs = ['src/main/resources']
            exclude 'file.txt'
        }
    }
}

4. find how to what is an uberjar. Make changes so you can use commons lang3 StringUtil in your jar. Make this uber jar executable. The output should be text but that should be using the StringUtils class of commons lang3


add dependency compile 'org.apache.commons:commons-lang3:3.6'
add task uberjar as below

task uberjar(type: Jar, dependsOn: [':compileJava', ':processResources']) {
    from files(sourceSets.main.output.classesDir)
    from configurations.runtime.asFileTree.files.collect { zipTree(it) }

    manifest {
        attributes 'Main-Class': 'abc'
    }
} 

5. Find a maven repository and add it as a repository in your build.gradle. You can use bintray, jcenter or any other repository. The goal is to learn how to use a custom repository For adding repository add below code. Using Maven Central

repositories {
    mavenCentral()
}

dependencies {
    compile 'org.hibernate:hibernate-core:3.6.7.Final'


}

6. Write a task in file "mytasks.gradle" and use it in your build.gradle. The goal is to be able to use tasks from another file in your build.gradle For using Task from external source add below code.

Apply from : ‘<file_name>’
