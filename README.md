# hello-swig
Beginner guide to [Swig](http://www.swig.org). SWIG is a software development tool that simplifies the task of interfacing different languages to C and C++ programs. In a nutshell, SWIG is a compiler that takes C/C++ declarations and creates the wrappers needed to access those declarations from other languages including Perl, Python, Tcl, Ruby, Guile, and Java. SWIG normally requires no modifications to existing code and can often be used to build a usable interface in only a few minutes.

# Steps

## 1. Simple c/cpp program
Create a "c" or "cpp" program file
- ex: `example.c`
- Add few methods

## 2. SWIG interface file
Create a SWIG interface ".i" file
- ex: `example.i`
- Add **function prototypes** and **variable declarations**

## 3. SWIG command
Use `swig` command to generate `java` file

```swig -java example.i```

- This will generate 3 files
    1. example_wrap.c
    2. example.java
    3. exampleJNI.java

## 4. Create a shared lib
- compile `example.c` and `example_wrap.c` using

```gcc -fPIC -I/usr/lib/jvm/java-1.8.0-openjdk-amd64/include/ -I/usr/lib/jvm/java-1.8.0-openjdk-amd64/include/linux -shared -o libexample.so example.c example_wrap.c```

- This will output the shared lib `libexample.so`


## 5. Access the shared lib inside java program (client)
- Create a `Java` client to code access the `C` program
- ex: `TestClient.java`
- compile the java file by

```javac TestClient.java```

- run the program by

```java -Djava.library.path=. TestClient```


## References
1. http://www.swig.org/Doc3.0/Introduction.html#Introduction_nn4
2. http://web.mit.edu/svn/src/swig-1.3.25/Examples/java/simple/index.html
3. https://anyline.com/news/java-c-swig-type-maps/ [advanced]
