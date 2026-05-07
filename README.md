# Ransomware-Sim
That is ransomware simulator in russian language (voice and maybe some things) i made it with deepseek in two days but I did most of the work myself
UPD: actually guys to launch that sim u need to disable windows defender because it blocks install of simulator and don't gives to launch sim
WARNING: UNLOCK CODE IS: UNLOCK-BTC-300, THAT FILE IS ONLY A SIMULATOR FOR EDUCATION, IF U GONNA WAIT 60 SECONDS UNTIL TIMEOUT OR WRITE THE CODE 3 TIMES WRONG THEN WINDOWS GONNA RESTART (like on/off/on)
GUYS I'M NOT A HACKER OR SMTH SO U CAN ACTUALLY TRUST ME, THERE IS MY OPEN-SOURCE CODE FOR THAT "RANSOM" (u actually can change da code if u want, change text for voice or smth BUT IF U CHANGED CODE AND REUPLOADED THAT THING ACTUALLY WRITE THAT I'M ORIGINAL AUTHOR):

Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing
Add-Type -AssemblyName System.Speech

$userMessage = "Ваш сын смотрит порно"

$speech = New-Object System.Speech.Synthesis.SpeechSynthesizer
$speech.Rate = -1
$speech.Volume = 100

$secret = "UNLOCK-BTC-300"
$timeoutSeconds = 60

$form = New-Object System.Windows.Forms.Form
$form.Text = ""
$form.WindowState = "Maximized"
$form.FormBorderStyle = "None"
$form.TopMost = $true
$form.ControlBox = $false
$form.KeyPreview = $true
$form.BackColor = [System.Drawing.Color]::Black

$form.Add_KeyDown({
    if ($_.Alt -and $_.KeyCode -eq "F4") {
        $_.SuppressKeyPress = $true
    }
})

# Картинка черепа
$imageUrl = "https://media.kasperskydaily.com/wp-content/uploads/sites/90/2016/04/06042356/petya-ransomware-featured-2-1-700x459.png"
$imagePath = "$env:TEMP\petya_skull.png"
try {
    Invoke-WebRequest -Uri $imageUrl -OutFile $imagePath -ErrorAction Stop
    $pictureBox = New-Object System.Windows.Forms.PictureBox
    $pictureBox.Image = [System.Drawing.Image]::FromFile($imagePath)
    $pictureBox.SizeMode = [System.Windows.Forms.PictureBoxSizeMode]::Zoom
    $pictureBox.Width = 300
    $pictureBox.Height = 150
    $pictureBox.Left = 20
    $pictureBox.Top = 20
    $form.Controls.Add($pictureBox)
} catch {}

# Получаем реальный курс биткоина
$btcPrice = "N/A"
try {
    $btcData = Invoke-RestMethod -Uri "https://api.coinpaprika.com/v1/tickers/btc-bitcoin" -ErrorAction Stop
    $btcPrice = [math]::Round($btcData.quotes.USD.price, 2)
} catch {}

$mainLabel = New-Object System.Windows.Forms.Label
$mainLabel.Text = "YOUR FILES ARE ENCRYPTED WITH AES-256"
$mainLabel.ForeColor = [System.Drawing.Color]::Red
$mainLabel.Font = New-Object System.Drawing.Font("Consolas", 20, [System.Drawing.FontStyle]::Bold)
$mainLabel.AutoSize = $true
$mainLabel.BackColor = [System.Drawing.Color]::Black

$subLabel = New-Object System.Windows.Forms.Label
$subLabel.Text = "SEND 300 USD IN BITCOIN TO:`n1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa"
$subLabel.ForeColor = [System.Drawing.Color]::Red
$subLabel.Font = New-Object System.Drawing.Font("Consolas", 14, [System.Drawing.FontStyle]::Bold)
$subLabel.AutoSize = $true
$subLabel.BackColor = [System.Drawing.Color]::Black

$btcLabel = New-Object System.Windows.Forms.Label
$btcLabel.Text = "BTC/USD: $btcPrice`nAmount to send: $([math]::Round(300 / (if ($btcPrice -ne "N/A") { [double]$btcPrice } else { 1 }), 8)) BTC"
$btcLabel.ForeColor = [System.Drawing.Color]::Red
$btcLabel.Font = New-Object System.Drawing.Font("Consolas", 12, [System.Drawing.FontStyle]::Regular)
$btcLabel.AutoSize = $true
$btcLabel.BackColor = [System.Drawing.Color]::Black

$warningLabel = New-Object System.Windows.Forms.Label
$warningLabel.Text = "DO NOT TURN OFF YOUR PC. ALL YOUR DOCUMENTS, PHOTOS, AND DATABASES WILL BE LOST FOREVER IF YOU ENTER THE WRONG CODE 3 TIMES."
$warningLabel.ForeColor = [System.Drawing.Color]::Red
$warningLabel.Font = New-Object System.Drawing.Font("Consolas", 10, [System.Drawing.FontStyle]::Bold)
$warningLabel.AutoSize = $true
$warningLabel.BackColor = [System.Drawing.Color]::Black

$timerLabel = New-Object System.Windows.Forms.Label
$timerLabel.ForeColor = [System.Drawing.Color]::Red
$timerLabel.Font = New-Object System.Drawing.Font("Consolas", 14, [System.Drawing.FontStyle]::Bold)
$timerLabel.AutoSize = $true
$timerLabel.BackColor = [System.Drawing.Color]::Black

$inputBox = New-Object System.Windows.Forms.TextBox
$inputBox.Font = New-Object System.Drawing.Font("Consolas", 14)
$inputBox.Size = New-Object System.Drawing.Size(300, 30)
$inputBox.BackColor = [System.Drawing.Color]::White
$inputBox.TextAlign = "Center"

$unlockButton = New-Object System.Windows.Forms.Button
$unlockButton.Text = "UNLOCK"
$unlockButton.Font = New-Object System.Drawing.Font("Consolas", 10)
$unlockButton.Size = New-Object System.Drawing.Size(150, 40)
$unlockButton.BackColor = [System.Drawing.Color]::DarkRed
$unlockButton.ForeColor = [System.Drawing.Color]::White
$unlockButton.FlatStyle = [System.Windows.Forms.FlatStyle]::Flat

$form.Controls.Add($mainLabel)
$form.Controls.Add($subLabel)
$form.Controls.Add($btcLabel)
$form.Controls.Add($warningLabel)
$form.Controls.Add($timerLabel)
$form.Controls.Add($inputBox)
$form.Controls.Add($unlockButton)

$form.Add_Shown({
    $mainLabel.Left = ($form.ClientSize.Width - $mainLabel.Width) / 2
    $mainLabel.Top = ($form.ClientSize.Height / 2) - 200
    $subLabel.Left = ($form.ClientSize.Width - $subLabel.Width) / 2
    $subLabel.Top = $mainLabel.Bottom + 20
    $btcLabel.Left = ($form.ClientSize.Width - $btcLabel.Width) / 2
    $btcLabel.Top = $subLabel.Bottom + 15
    $warningLabel.Left = ($form.ClientSize.Width - $warningLabel.Width) / 2
    $warningLabel.Top = $btcLabel.Bottom + 25
    $timerLabel.Left = ($form.ClientSize.Width - $timerLabel.Width) / 2
    $timerLabel.Top = $warningLabel.Bottom + 30
    $inputBox.Left = ($form.ClientSize.Width - $inputBox.Width) / 2
    $inputBox.Top = $timerLabel.Bottom + 30
    $unlockButton.Left = ($form.ClientSize.Width - $unlockButton.Width) / 2
    $unlockButton.Top = $inputBox.Bottom + 30
})

# --- Голос и таймер ---
$startTime = Get-Date
function Stop-VoiceAndTimer {
    $voiceTimer.Stop()
    $speech.Dispose()
}

$speech.SpeakAsync($userMessage)

$voiceTimer = New-Object System.Windows.Forms.Timer
$voiceTimer.Interval = 8000
$voiceTimer.Add_Tick({
    $speech.SpeakAsync($userMessage)
})
$voiceTimer.Start()

$timer = New-Object System.Windows.Forms.Timer
$timer.Interval = 1000
$timer.Add_Tick({
    $remaining = $timeoutSeconds - [int]((Get-Date) - $startTime).TotalSeconds
    if ($remaining -le 0) {
        $timer.Stop()
        Stop-VoiceAndTimer
        $form.Close()
        shutdown /r /f /t 2
    } else {
        $timerLabel.Text = "TIME REMAINING: $remaining SECONDS"
        $timerLabel.Left = ($form.ClientSize.Width - $timerLabel.Width) / 2
        if ($timerLabel.ForeColor -eq [System.Drawing.Color]::Red) {
            $timerLabel.ForeColor = [System.Drawing.Color]::OrangeRed
        } else {
            $timerLabel.ForeColor = [System.Drawing.Color]::Red
        }
    }
})
$timer.Start()

# --- Кнопка разблокировки ИСПРАВЛЕНА ---
$unlockButton.Tag = 0
$maxAttempts = 3

$unlockButton.Add_Click({
    if ($inputBox.Text -eq $secret) {
        $timer.Stop()
        Stop-VoiceAndTimer
        $form.Close()
    } else {
        # Увеличиваем счётчик, который хранится в свойстве Tag кнопки
        $unlockButton.Tag = [int]$unlockButton.Tag + 1
        $attempts = $unlockButton.Tag

        if ($attempts -ge $maxAttempts) {
            $timer.Stop()
            Stop-VoiceAndTimer
            $form.Close()
            shutdown /r /f /t 2
        } else {
            $remainingAttempts = $maxAttempts - $attempts
            [System.Windows.Forms.MessageBox]::Show("WRONG CODE!`nYou have $remainingAttempts attempts left.", "ACCESS DENIED", [System.Windows.Forms.MessageBoxButtons]::OK, [System.Windows.Forms.MessageBoxIcon]::Error)
            $inputBox.Text = ""
        }
    }
})

$form.ShowDialog()
