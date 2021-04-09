https://rubygarage.org/blog/ruby-on-rails-web-application-vulnerabilities-how-to-make-your-app-secure

# Command Injection Flaws 

Your application may be vulnerable to command injection attacks if it needs to execute some commands in the underlying operating system.
Ruby offers several methods to do execute such commands: exec(command), syscall(command), system(command), and command. These functions require your particular attention since users may be able to enter the whole command or at least part of it.
Keep in mind that in most shells, it's possible to execute another command after the first one if they are chained with the help of a vertical bar (|) or a semicolon (;).



To fend off such attacks, you should use system(command, parameters), which provides a safe way to pass command line parameters.
Another potential danger is an ImageMagick command injection. When this software is used, Rails passes command line arguments to an executable. However, the arguments can be modified in order to force ImageMagick to overload the CPU. Eventually, this may lead to a server failure.
To protect your app from this kind of attack, validate user input against regex. You can use the Dragonfly gem to check user arguments.
