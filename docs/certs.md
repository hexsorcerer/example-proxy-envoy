You'll need to generate 2 different certificates; one for the ASP.NET Core service, and one for envoy.

# Generate the ASP.NET Core web API certificate

The full official version can be found [here](https://docs.microsoft.com/en-us/aspnet/core/security/docker-https?view=aspnetcore-2.2)

```
dotnet dev-certs https -ep %USERPROFILE%\.aspnet\https\example-api.pfx -p <password>
```

This command will create the certificate for you. If you create it somewhere else, you'll have to update the docker-compose file with the new paths.

Don't forget to add the password you set here to your src/.env file!
```
dotnet dev-certs https --trust
```

This command will add the certificate you just generated to the trusted store on your machine. You'll probably get a prompt asking you to allow it.

If at some point you feel like you messed up and want to start over, just delete the .pfx file and run this command:
```
dotnet dev-certs https --clean
```

This will remove any previously trusted cert, and now you can just make a new one and trust it again.

# Generate the Envoy certificate

This one was a tiny bit harder. Here's quick and dirty instructions with links to the fulls docs so you can read up on each one more if you want.

First make sure you have a newer [PowerShell](https://github.com/PowerShell/PowerShell/releases)

Now, open a new PowerShell administrative shell, and install [Chocolately](https://chocolatey.org/install)

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Once you have Chocolatey installed, you can now install a tool call [mkcert](https://github.com/FiloSottile/mkcert)

```
choco install mkcert
```

This tool makes this part a lot easier because it generates the certificate and key you need, plus it will automatically import it into the trusted store for you.

```
mkcert.exe -key-file envoy-key.pem -cert-file envoy-cert.pem localhost *.localhost
```

Run this command in your $env:USERPROFILE/.aspnet/https directory, or you can update the docker-compose file if you choose to make it somewhere else.

# Done

You should be good to go on certs now.