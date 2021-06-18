Git on the Server

# Intro

- In order to do any collaboration in Git, you’ll need to have a _remote Git repository_.
- Although you can technically push changes to and pull changes from _individuals' repositories_, doing so is **discouraged** because you can fairly easily confuse what they’re working on if you’re not careful.
- Furthermore, you want your _collaborators_ to be able to _access the repository_ even if your computer is offline — having a more reliable _common repository_ is often **useful**.
- Therefore, the _preferred method for collaborating with someone_ is to set up an intermediate repository that you both have access to, and push to and pull from that.
- Running a __Git server__ is fairly _straightforward_:
1. You choose which __protocols__ you want your server to support
2. Some typical __setups using those protocols__ and how to __get your server running__ with them
3. Go over a few hosted options

## The Protocols
- Git can use four distinct protocols to transfer data: 
1. **Local** 
2. **HTTP** 
3. **Secure Shell (SSH)**
4. **Git**

### Local Protocol
- The **most basic** is the _Local protocol_, in which the remote repository is in another directory on the same host.
- This is often used if everyone on your team has access to a __shared filesystem__ such as an __NFS__ mount, or in the less likely case that __everyone logs in to the same computer__.
- The __latter wouldn’t be ideal__, because all your code repository instances would reside on the same computer, making a __catastrophic loss much more likely__.
- If you have a __shared mounted filesystem__, then you can **clone**, **push** to, and **pull** from a local file based repository.
- To clone a local repository, you can run something like this:
`$ git clone /srv/git/project.git`
OR
`$ git clone file:///srv/git/project.git`
- If you **just specify the path**, Git tries to *use hardlinks* or *directly copy the files it needs*. it is **faster**.
- But Git operates _slightly differently_ if you explicitly specify `file://` at the beginning of the URL.
- In `file://` case, Git fires up the processes that it normally uses to transfer data over a network, which is generally _much less efficient_.
- The _main reason_ to specify the `file://` prefix is if you __want a clean copy of the repository__ with _extraneous references or objects left out_ — generally after an import from another VCS or something similar

__The Pros__

- They’re simple and they use existing file permissions and network access.
- If you already have a shared filesystem, setting up a repository is very easy.
- Stick the bare repository copy somewhere everyone has shared access to and set the read/write permissions as you would for any other shared directory.

__The Cons__

- Shared access is generally more difficult to set up and reach from multiple locations than basic network access.
- Slow compared to network-based access
- you have to mount the remote disk, f you want to push from your laptop when you’re at home
- A repository on NFS is often slower than the repository over SSH on the same server
- Does not protect the repository against accidental damage
- Every user has full shell access to the “remote” directory, and there is nothing preventing them from changing or removing internal Git files and corrupting the repository.

### The HTTP Protocols

