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
(such as Spring) in their code. The stack traces in these cases are
usually huge (think hundreds of lines long) and add to it the fact
that the exceptions are usually chained so there is one exception
leading to the other so on and so forth. Moreover, for each exception,
majority of lines in the trace would refer to framework classes rather
than to our own code. 

When we are looking to identify a problem, we are usually interested
in our own classes as problems usually lie in our business logic
rather than in framework. So when one looks at these gigantic traces,
one would be usually hunting for own class names. You will see
developers frantically staring at the trace and scrolling up and down
to cover all the chained exceptions. 

Having suffered this for a short while, I decided to solve it by
writing a script. The requirements are very simple. Remove every line
in the stack trace that doesn't refer to our classes, with a small
caveat. Keep the first line of every exception irrespective of whether
the line refers to our class or not. This is becase some exceptions in
the chair are going to be from framework classes and it helps to have
some information about the exception in these cases. 

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
    


