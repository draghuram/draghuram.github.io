
I am a big proponent of automating daily routine tasks but I have a
slightly different take when it comes to building development
environments. I think it is ok not to build a completely ready dev env
image (for new developers who are joining the team). It is perfectly
ok to say that all you need is a Linux distro with the following tools
(with specific or minimum versions). Why? Some people may argue that
it is much easier to onboard new developers if we have an "official"
dev env and not all developers are comfortable installing tools on
their own. I would say that if a developer is not comfortable building
their own dev environment, they are not really serious developers. If
you are coding in Go, you should have no problem installing
it. Similarly, if you write tests in Python using pytest framework,
you should be capable of creating a virtual environment and installing
pytest and any other dependencies. Yes, some of the installation steps
may be involved and may even be painful but I don't think developers
should be shielded from it.

I am not saying that every developer should be free to use whatever
tools they want to and whatever versions they can. On the contrary,
the build script should explicitly check that all the tools needed for
the project are available (including checks for versions). If there is
any tool missing or if the version is not accurate, the script should
give a clear message possibly including instructions on how to
install. 

So on one hand, we are not building an "official" image for dev
environment though we can set some guidelines such as "we support only
Linux as dev environment". But we also have a build script that does
very thorough checks of the tools and their versions. I think this
combination is getting best of both the worlds. 
