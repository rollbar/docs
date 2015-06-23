<span class="date">06/11/14 at 11:03 PM</span>

Here's an MSBuild target to notify Rollbar of a publish. Requires
[RollbarSharp](https://github.com/mroach/RollbarSharp) web.config
entries, and git on your PATH.

``` {data-language="xml"}
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Target Name="NotifyRollbarOfDeploy" AfterTargets="MSDeployPublish">
    <XmlPeek XmlInputPath="$(_PackageTempDir)\web.config" 
             Query="//appSettings/add[@key='Rollbar.AccessToken']/@value">
      <Output TaskParameter="Result" ItemName="RollbarAccessToken" />
    </XmlPeek>
    <XmlPeek XmlInputPath="$(_PackageTempDir)\web.config" 
             Query="//appSettings/add[@key='Rollbar.Environment']/@value">
      <Output TaskParameter="Result" ItemName="RollbarEnvironment" />
    </XmlPeek>
    <Exec Command="git log -1 --format=%%H" ConsoleToMSBuild="true" EchoOff="true" WorkingDirectory="$(ProjectDir)\..">
      <Output TaskParameter="ConsoleOutput" PropertyName="GitSHA" />
    </Exec>
    <Exec Command="git config user.email" ConsoleToMSBuild="true" EchoOff="true" WorkingDirectory="$(ProjectDir)\..">
      <Output TaskParameter="ConsoleOutput" PropertyName="GitEmail" />
    </Exec>

    <Message Text="Rollbar.AccessToken: @(RollbarAccessToken)" Importance="Normal" />
    <Message Text="Rollbar.Environment: @(RollbarEnvironment)" Importance="Normal" />
    <Message Text="Git SHA: $(GitSHA)" Importance="Normal" />
    <Message Text="Rollbar: $(GitEmail) deployed @(RollbarEnvironment) revision $(GitSHA)" Importance="High" />
    <Exec Command="@powershell -NoProfile -ExecutionPolicy unrestricted -Command &quot;(new-object net.webclient).UploadString('https://api.rollbar.com/api/1/deploy/', 'access_token=@(RollbarAccessToken)&amp;environment=@(RollbarEnvironment)&amp;revision=$(GitSHA)&amp;local_username=$(GitEmail)')&quot;" EchoOff="true" />
  </Target>
</Project>
```

Thanks to [@barake](https://github.com/barake) for putting this together
originally as a
[gist](https://gist.github.com/barake/128a094153d64ff5e230).
