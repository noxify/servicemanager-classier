# servicemanager-classier

This class extending engine is a fork from https://github.com/ironboy/classier.

It includes only the required changes to make it work inside the service manager.

A detailed description how this engine works is available here: https://classier.cloudeducation.se/


# Limitations

* You have to define the `_class` variable, because the service manager has no DOM or something else which is required to use the existing functionality from the classier engine
