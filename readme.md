### JAVA
java -version

### copy build.xml into SimpleDB_3.4/simpledb/

```
<?xml version="1.0" encoding="UTF-8"?>
<project name="SimpleDB" default="compile" basedir=".">
    <description>
        Build script for the SimpleDB project.
    </description>

    <!-- Define global properties -->
    <property name="src.dir" value="."/>
    <property name="build.dir" value="bin"/>

    <!-- Clean the build directory -->
    <target name="clean">
        <delete dir="${build.dir}"/>
    </target>

    <!-- Initialize the build directory -->
    <target name="init">
        <mkdir dir="${build.dir}"/>
    </target>

    <!-- Compile the Java source files -->
    <target name="compile" depends="init">
        <javac srcdir="${src.dir}"
               destdir="${build.dir}"
               includeAntRuntime="false"
               debug="true"
               source="1.8"
               target="1.8">

            <!-- Include all Java files in subdirectories -->
            <include name="**/*.java"/>
            <!-- Exclude any test files if necessary -->
            <!-- <exclude name="**/*Test.java"/> -->

            <!-- Set the classpath if there are external libraries -->
            <!--
            <classpath>
                <fileset dir="lib">
                    <include name="**/*.jar"/>
                </fileset>
            </classpath>
            -->
        </javac>
    </target>

    <!-- Run the main class -->
    <target name="run" depends="compile">
        <java classname="simpledb.server.StartServer" fork="true">
            <classpath>
                <pathelement path="${build.dir}"/>
                <!-- Include any additional classpath entries if needed -->
            </classpath>
            <!-- Pass any arguments to the main class here -->
            <!-- <arg value="argument_value"/> -->
        </java>
    </target>

    <!-- Clean and rebuild the project -->
    <target name="rebuild" depends="clean,compile"/>
</project>
```

### Ant compile, run
```
brew install ant

ant compile

ant run
```
