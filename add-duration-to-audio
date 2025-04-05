tell application "DEVONthink"
	set theRecords to selected records
	repeat with theRecord in theRecords
		set thePath to path of theRecord
		if thePath is not "" and type of theRecord is not group then
			set fileExtension to do shell script "echo " & quoted form of thePath & " | awk -F. '{print tolower($NF)}'"
			set audioExtensions to {"mp3", "wav", "aac", "m4a", "flac", "ogg", "wma", "aiff", "alac", "caf"}
			
			if audioExtensions contains fileExtension then
				set durationCmd to "afinfo " & quoted form of thePath & " | grep duration | awk '{print $3}'"
				try
					set theDuration to do shell script durationCmd
					-- Более надежное округление до двух знаков
					set durationCmd2 to "echo " & theDuration & " | awk '{printf \"%.2f\", $1}'"
					set roundedDuration to do shell script durationCmd2
					add custom meta data roundedDuration for "Duration" to theRecord
				on error errMsg
					log "Processing error " & thePath & ": " & errMsg
				end try
			end if
		end if
	end repeat
end tell
