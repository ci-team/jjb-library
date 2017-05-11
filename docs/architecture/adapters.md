Adapters
========

This repository is supposed to support different SCM systems.

To avoid duplication of jobs, templates and other things, we introduce adapters that connect SCM-specific triggers, 
parameters and publishers with universal building blocks.

So in general every relatively standard template should look as follow:

```yaml
- job-template:
    id: '<some-id>'
    name: '<some name>'
    
    parameters:
    - library/<gitserver-type>/parameters
    
    triggers:
    - library/<gitserver-type>/trigger
    
    scm:
    - library/<gitserver-type>/scm
    
    builders:
    - library/<gitserver-type>/adapter
    # after this point we work with universally
    # translated environment variables
    
    - some-universal-building-block
    - some-other-universal-building-block
    
    publishers:
    - library/<gitserver-type>/publisher
```

And for more complicated cases it's ok to have additional entities which are
not bound to particular SCM.

```yaml
- job-template:
    id: '<some-id>'
    name: '<some name>'
    
    parameters:
    - library/<gitserver-type>/parameters
    - some-universal-additional-parameters
    
    triggers:
    - library/<gitserver-type>/trigger
    - some-universal-additional-triggers
    
    scm:
    - library/<gitserver-type>/scm
    - some-universal-additional-scms
    
    builders:
    - library/<gitserver-type>/adapter
    # after this point we work with universally
    # translated environment variables
    
    - some-universal-building-block-1
    - some-universal-building-block-2
    
    publishers:
    - library/<gitserver-type>/publisher
    - some-universal-publisher
```
