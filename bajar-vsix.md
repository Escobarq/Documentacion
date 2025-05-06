# Script: descargar-vsix.ps1
param (
    [string]$url,
    [string]$version
)

if (-not $url -or -not $version) {
    Write-Host "Uso: .\descargar-vsix.ps1 <url-del-marketplace> <version>"
    exit 1
}

## Extraer el itemName de la URL
if ($url -match "itemName=([^&]+)") {
    $itemName = $matches[1]
} else {
    Write-Host "No se pudo extraer itemName de la URL."
    exit 1
}

## Separar en publisher y nombre de la extensiÃ³n
if ($itemName -match "^([^\.]+)\.(.+)$") {
    $fieldA = $matches[1]
    $fieldB = $matches[2]
} else {
    Write-Host "Formato de itemName invÃ¡lido."
    exit 1
}

# Construir la URL de descarga
$downloadUrl = "https://marketplace.visualstudio.com/_apis/public/gallery/publishers/$fieldA/vsextensions/$fieldB/$version/vspackage"

## COMPLETO
```powershell
param (
    [string]$url,
    [string]$version
)

if (-not $url -or -not $version) {
    Write-Host "Uso: .\descargar-vsix.ps1 <url> <version>"
    exit 1
}

# Extraer el itemName de la URL
if ($url -match "itemName=([^&]+)") {
    $itemName = $matches[1]
} else {
    Write-Host "No se pudo extraer itemName de la URL."
    exit 1
}

# Separar en publisher y nombre de la extensión
if ($itemName -match "^([^.]+)\.(.+)$") {
    $publisher = $matches[1]
    $extensionName = $matches[2]
} else {
    Write-Host "Formato de itemName inválido."
    exit 1
}

# Construir la URL de descarga
$downloadUrl = "https://marketplace.visualstudio.com/_apis/public/gallery/publishers/$publisher/vsextensions/$extensionName/$version/vspackage"

# Descargar el archivo .vsix
$vsixFile = "$extensionName-$version.vsix"
Write-Host "Descargando $downloadUrl ..."
Invoke-WebRequest -Uri $downloadUrl -OutFile $vsixFile

Write-Host "Descarga completada: $vsixFile"
```

# Descargar el archivo .vsix
$vsixFile = "$fieldB-$version.vsix"
Write-Host "Descargando $downloadUrl ..."
Invoke-WebRequest -Uri $downloadUrl -OutFile $vsixFile

Write-Host "Descarga completada: $vsixFile"
