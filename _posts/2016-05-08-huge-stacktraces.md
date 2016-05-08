---
layout: post
title:  "Huge Stacktraces..."
date:   2016-05-06
categories: debugging stacktrace java python
---

Dealing with stack traces is a fact of life for many developers. In
fact, not a day goes by that I don't need to stare at one and
make sense of it. Stacktraces are extremely useful in locating the
exact place in the code where the problem occurred. However, there is
a downside that is clearly apparent to any one who uses frameworks
(especially in Java, such as Spring) in their code. The stack traces
in these cases are usually huge, even though, majority of lines in these
traces would refer to framework classes rather than to our own code.

When we are looking to identify a problem in our business logic, we
are usually interested in our own classes. So you can see developers
frantically staring at these gigantic traces and scrolling up and
down, in order to locate their own classes in all those multitude of
lines. 

Having suffered this for a short while, I decided to solve the problem
by writing a script. The requirements are very simple. Remove every line
in the stack trace that doesn't refer to our classes, with a small
caveat. Keep the first line of every exception irrespective of whether
the line refers to our class or not. This is becase it helps to have
some minimal information about every exception int he chain. 

You can find the python script 

You can see the result of the script below:
    
    Context initialization failed org.springframework.beans.factory.CannotLoadBeanClassException: Error loading class [com.example.ResourceHandler] for bean with name 'testResourceHandler' defined in ServletContext resource [/WEB-INF/applicationContext.xml]: problem with class file or dependent class; nested exception is java.lang.NoClassDefFoundError: com.example.ResourceHandler not found from bundle [com.example.test (com.example.test)]
    	at org.springframework.beans.factory.support.AbstractBeanFactory.resolveBeanClass(AbstractBeanFactory.java:1272)
            ...
    Caused by: java.lang.NoClassDefFoundError: com.example.ResourceHandler not found from bundle [com.example.test (com.example.test)]
    	at org.eclipse.gemini.blueprint.util.BundleDelegatingClassLoader.findClass(BundleDelegatingClassLoader.java:110)
            ...
    	... 32 common frames omitted
    Caused by: org.eclipse.virgo.kernel.osgi.framework.ExtendedNoClassDefFoundError: com/example/ResourceHandler in KernelBundleClassLoader: [bundle=com.example.test_2.4.0.201605061424] in KernelBundleClassLoader: [bundle=com.example.test_2.4.0.201605061424]
    	at org.eclipse.virgo.kernel.userregion.internal.equinox.KernelBundleClassLoader.loadClass(KernelBundleClassLoader.java:152)
            ...
    	... 38 common frames omitted
    Caused by: org.eclipse.virgo.kernel.osgi.framework.ExtendedNoClassDefFoundError: com/example/ResourceHandler in KernelBundleClassLoader: [bundle=com.example.test_2.4.0.201605061424]
    	at org.eclipse.virgo.kernel.userregion.internal.equinox.KernelBundleClassLoader.defineClass(KernelBundleClassLoader.java:255)
            ...
    	... 43 common frames omitted
    Caused by: java.lang.NoClassDefFoundError: com/example/ResourceHandler
    	at java.lang.ClassLoader.defineClass1(Native Method)
            ...
    	... 55 common frames omitted
    Caused by: org.eclipse.virgo.kernel.osgi.framework.ExtendedClassNotFoundException: com.example.ResourceHandler in KernelBundleClassLoader: [bundle=com.example.test_2.4.0.201605061424]
    	at org.eclipse.virgo.kernel.userregion.internal.equinox.KernelBundleClassLoader.loadClass(KernelBundleClassLoader.java:150)
            ...
    	... 59 common frames omitted
    Caused by: java.lang.ClassNotFoundException: com.example.ResourceHandler
    	at org.eclipse.osgi.internal.loader.BundleLoader.findClassInternal(BundleLoader.java:455)
            ...
    	... 60 common frames omitted

Another example:

    com.example.AuthorizationException: null
    	at com.example.UserHelperImpl.deleteUser(UserHelperImpl.java:95)
    	at com.example.UserController.deleteUser(UserController.java:316)
            ...
    	at com.example.LicenseFilter.doFilter(LicenseFilter.java:42)
            ...
    	at com.example.SecurityFilter.doFilter(SecurityFilter.java:224)
            ...
    
    
