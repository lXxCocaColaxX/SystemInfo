<#
.SYNOPSIS
    Muestra información del sistema (hardware, red y discos)
#>

function Show-Header {
    Clear-Host
    Write-Host -ForegroundColor Blue "          _____           _   _ _____ _____  ___  "
    Write-Host -ForegroundColor Cyan "         /  ___|         | | | |_   _|  ___|/ _ \ "
    Write-Host -ForegroundColor Blue "         \ \`--. _   _ ___| |_| | | | | |__ / /_\ \"
    Write-Host -ForegroundColor Cyan "          \`--. \ | | / __|  _  | | | |  __||  _  |"
    Write-Host -ForegroundColor Blue "         /\__/ / |_| \__ \ | | |_| |_| |___| | | |"
    Write-Host -ForegroundColor Cyan "         \____/ \__, |___\_| |_/\___/\____/\_| |_/"
    Write-Host -ForegroundColor Blue "                 __/ |                           "
    Write-Host -ForegroundColor Cyan "                |___/                            "
    Write-Host ""
}

function Get-SystemInfo {
    # Hardware
    $os = (Get-CimInstance Win32_OperatingSystem).Caption
    $cpu = (Get-CimInstance Win32_Processor).Name
    $ram = [math]::Round((Get-CimInstance Win32_PhysicalMemory | Measure-Object -Property Capacity -Sum).Sum /1GB, 2)
    $gpu = (Get-CimInstance Win32_VideoController).Name
    
    # Red
    $ip = (Get-NetIPAddress -AddressFamily IPv4 | Where-Object {
        $_.InterfaceAlias -match "Ethernet|Wi-Fi" -and $_.IPAddress -ne "127.0.0.1"
    }).IPAddress
    
    # Discos
    $discos = Get-CimInstance Win32_LogicalDisk | Where-Object {$_.DriveType -eq 3}

    # Mostrar info
    Write-Host -ForegroundColor Yellow "`n[🖥️ Sistema Operativo]" -NoNewline
    Write-Host " $os"
    Write-Host -ForegroundColor Yellow "`n[⚡ Procesador]" -NoNewline
    Write-Host " $cpu"
    Write-Host -ForegroundColor Yellow "`n[💾 Memoria RAM]" -NoNewline
    Write-Host " $ram GB"
    Write-Host -ForegroundColor Yellow "`n[🎮 Gráficos]" -NoNewline
    Write-Host " $gpu"
    Write-Host -ForegroundColor Yellow "`n[🌐 Dirección IP]" -NoNewline
    Write-Host " $ip"
    Write-Host -ForegroundColor Yellow "`n[💽 Discos]"
    foreach ($disco in $discos) {
        $free = [math]::Round($disco.FreeSpace/1GB, 2)
        $total = [math]::Round($disco.Size/1GB, 2)
        Write-Host " $($disco.DeviceID): $free GB libres de $total GB"
    }
}

# Ejecutar
Show-Header
Get-SystemInfo
Read-Host "`nPresiona Enter para salir..."
