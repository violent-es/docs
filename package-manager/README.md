# Package Manager

The package manager will fetch dependencies from the entry point by collecting all related `include` directives (that do not start with `.`):

```
include 'com.framework.core@0.1.0';
```

This will then allow all scripts in the project to use public definitions from a library and `import` them.