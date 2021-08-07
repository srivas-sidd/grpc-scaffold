# grpc-scaffold
Tools that generates skeleton files and folders, server and client code to be used in Grpc projects.

<h3>Installation</h3>

Install the library by running the following command

<br>

```

python -m pip install grpc-scaffold-0.0.3.tar.gz 
```


<h3>Usage</h3>

<br>
There are two commands that you can run. First one generates the standard folder structure used at Delphai. The command to do that is
<br>
<br>

```

python -m GrpcScaffold.generate_skeleton --path "path_to_project"  --workflow utils review prodution destroy-review
```
<br>
--path path_to_project: Path where the skeleton has to be generated
<br><br>
--workflow: which workflow files to generate. Options are utils review production and destroy-review. A subset of these options will also do.
<br><br>

This will generate a folder structure like the following

```

├── .github/workflow                   
├── config                    
├── proto                     
├── src 
├── Dockerfile 
├── protodep.lock
├── protodep.toml
├── pyproject.lock
```
<br><br>
The second command generates server and client code. To do that you first have to save the proto file inside proto folder of project you have generated.
Then run the command
<br><br>
```

python -m GrpcScaffold.generate_files --proto path-to-proto --path root-path-to-project
```
<br>

--proto is the path to the proto file
<br><br>
--path is the path to the root folder of the project that contains proto and src folders
<br><br>
Things to keep in mind: The proto file should have the service definition in a single line.

```

service Foo {
  rpc bar(Req) returns(Res) {}
}
```
<br>
works, but 
<br>

```

service Foo {
  rpc bar(Req) 
    returns(Res) {}
}

```

<br>
Does not work. Comments are parsed properly.
