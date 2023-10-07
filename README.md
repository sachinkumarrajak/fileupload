[Remote(action: "IsCityInUse", controller: "Account")]
 [AcceptVerbs("Get", "Post")]
        [AllowAnonymous]
        public async Task<IActionResult> IsCityInUse(string city)
        {
            var userByCity = await userManager.Users.FirstOrDefaultAsync(u => u.City == city);

            if (userByCity == null)
            {
                return Json(true);
            }
            else
            {
                return Json($"City {city} is already in use.");
            }
        }
<?xml version="1.0" encoding="UTF-8"?>
<Wix xmlns="http://schemas.microsoft.com/wix/2006/wi">
  <Product Id="*" Name="SetupProject4" Language="1033" Version="1.0.0.0" Manufacturer="YourManufacturer" UpgradeCode="a4ff7dbc-867d-41c8-95c2-4d1622fda3dc">

    <Package InstallerVersion="200" Compressed="yes" InstallScope="perMachine" />

    <MajorUpgrade DowngradeErrorMessage="A newer version of [ProductName] is already installed." />

    <MediaTemplate EmbedCab="yes" />

    <Feature Id="MainApplication" Title="Main Application" Level="1">
      <ComponentGroupRef Id="ProductComponents" />
    </Feature>

    <Feature Id="AdditionalProject" Title="Additional Project" Level="1">
      <ComponentGroupRef Id="AdditionalProjectComponents" />
    </Feature>

    <Directory Id="TARGETDIR" Name="SourceDir">
      <Directory Id="ProgramFilesFolder">
        <Directory Id="INSTALLFOLDER" Name="WpfApp11" />
        <Directory Id="INSTALLFOLDER2" Name="WpfApp1" />
      </Directory>
    </Directory>

    <ComponentGroup Id="ProductComponents" Directory="INSTALLFOLDER">
      <Component Id="WpfApp11DepsJson" Guid="{e9afe82c-975d-40a1-8aed-308ba26a68f3}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp11\bin\Debug\net7.0-windows\WpfApp11.deps.json" />
      </Component>
      <Component Id="WpfApp11Dll" Guid="{e9afe82c-975d-40a1-8aed-308ba26a68f9}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp11\bin\Debug\net7.0-windows\WpfApp11.dll" />
      </Component>
      <Component Id="WpfApp11Exe" Guid="{e9afe82c-975d-40a1-8aed-308ba26a68f1}">
        <File Id="WpfApp11Exe" Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp11\bin\Debug\net7.0-windows\WpfApp11.exe" KeyPath="yes" />
      </Component>
      <Component Id="WpfApp11Pdb" Guid="{e9afe82c-975d-40a1-8aed-308ba26a68f5}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp11\bin\Debug\net7.0-windows\WpfApp11.pdb" />
      </Component>
      <Component Id="WpfApp11RuntimeConfig" Guid="{e9afe82c-975d-40a1-8aed-308ba26a68f7}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp11\bin\Debug\net7.0-windows\WpfApp11.runtimeconfig.json" />
      </Component>
      <!-- Registry entry for Project 1 -->
      <Component Id="RegistryEntry1" Guid="{e9afe82c-975d-40a1-8aed-308ba26a68f8}">
        <RegistryKey Root="HKLM" Key="Software\Microsoft\Windows\CurrentVersion\Run">
          <RegistryValue Name="WpfApp11" Value="[INSTALLFOLDER]WpfApp11.exe" Type="string" />
        </RegistryKey>
      </Component>
    </ComponentGroup>

    <!-- Components for the additional project -->
    <ComponentGroup Id="AdditionalProjectComponents" Directory="INSTALLFOLDER2">
      <Component Id="WpfApp1DepsJson" Guid="{e9afe82c-975d-40a1-8aed-308ba26a48f4}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp1\bin\Debug\net7.0-windows\WpfApp1.deps.json" />
      </Component>
      <Component Id="WpfApp1Dll" Guid="{e9afe82c-975d-40a1-8aed-308ba26a48f3}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp1\bin\Debug\net7.0-windows\WpfApp1.dll" />
      </Component>
      <Component Id="WpfApp1Exe" Guid="{e9afe82c-975d-40a1-8aed-308ba26a48f9}">
        <File Id="WpfApp1Exe" Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp1\bin\Debug\net7.0-windows\WpfApp1.exe" KeyPath="yes" />
      </Component>
      <Component Id="WpfApp1Pdb" Guid="{e9afe82c-975d-40a1-8aed-308ba26a6833}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp1\bin\Debug\net7.0-windows\WpfApp1.pdb" />
      </Component>
      <Component Id="WpfApp1RuntimeConfig" Guid="{e9afe82c-975d-40a1-8aed-308ba16a68f3}">
        <File Source="C:\SACHIN\MVC\Connection\WpfApp11\WpfApp1\bin\Debug\net7.0-windows\WpfApp1.runtimeconfig.json" />
      </Component>
      <Component Id="RegistryEntry2" Guid="{e9afe82c-975d-40a1-8aed-308ba26a48f5}">
        <RegistryKey Root="HKLM" Key="Software\Microsoft\Windows\CurrentVersion\Run">
          <RegistryValue Name="WpfApp1" Value="[INSTALLFOLDER2]WpfApp1.exe" Type="string" />
        </RegistryKey>
      </Component>
    </ComponentGroup>

    <!-- Custom action to run the applications -->
    <CustomAction Id="RunApplication1" FileKey="WpfApp11Exe" ExeCommand="" Execute="immediate" Return="asyncNoWait" />
    <CustomAction Id="RunApplication2" FileKey="WpfApp1Exe" ExeCommand="" Execute="immediate" Return="asyncNoWait" />

    <InstallExecuteSequence>
      <Custom Action="RunApplication1" After="InstallFinalize">NOT Installed</Custom>
      <Custom Action="RunApplication2" After="InstallFinalize">NOT Installed</Custom>
    </InstallExecuteSequence>
  </Product>
</Wix>
