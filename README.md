# Print
; Trim a pattern of characters from left '>', right '&lt;' or both ( '&lt;>' or '>&lt;' ) | Default trims from right  _Print( StringTrimPattern('####Trim from left####', '#', '>')) ;use '>' to trim from left _Print( StringTrimPattern('####Trim from right####', '#', '&lt;')) ;use '&lt;' to trim from right _Print( StringTrimPattern('####trim from both sides####', '#', '&lt;>')) ;use '&lt;>' or '>&lt;' to trim from both sides _Print( StringTrimPattern('_>&lt;_%__Advanced test from both sides_%%_/__', '%_&lt;>/', '&lt;>')) ;use '&lt;>' to trim from both sides _Print( StringTrimPattern('C:folder', '', '&lt;')) ;trim backslashes from right _Print( StringTrimPattern('C:folderimageSequence_005484.051', '0123456789._', '&lt;')) ;Trim image numbering _Print( StringTrimPattern('C:folderimageSequence_005484-051.tga', '0123456789abcdefghijklmnopqrstuvwxyz _-./', '&lt;')) ;Trim to root _Print( StringTrimPattern('C:folderimageSequence_005484-051.tga', 'abcdefghijklmnopqrituvwxyz:', '>')) ;Trim root _Print( StringTrimPattern('Remove trailing white spaces    ', ' ', '&lt;')) ;Trim white spaces _Print( StringTrimPattern('Remove new lines @CRLF' &amp; @CRLF &amp; @CRLF, @CRLF, '&lt;')) ;Trim new lines _Print( StringTrimPattern('Image.tga', 'tgajpgpng', '&lt;')) ;Trim various image file extentions _Print( StringTrimPattern('Image.jpg', 'tgajpgpng', '&lt;')) ;Trim various image file extentions _Print( StringTrimPattern('C:folderprogram.exe', 'ex', '&lt;')) ;Trim the extention _Print( StringTrimPattern('Non case SensitiveXXXxxx', 'x', '&lt;')) ;not case sensitive _Print( StringTrimPattern('Case SensitiveXXXxxx', 'x', '&lt;', 1)) ;case sense test (same options as StringCompare ) Exit  Func StringTrimPattern($sString, $sPattern, $sDirection = '&lt;', $iCaseSense = 0)     If $sDirection &lt;> '>' And $sDirection &lt;> '&lt;' And $sDirection &lt;> '&lt;>' And $sDirection &lt;> '>&lt;' Then         Return SetError(1, 0, "")     EndIf     Local $a, $b, $sChar     $a = StringSplit($sPattern, '')     $b = StringSplit($sDirection, '')     For $i = 1 To $b[0]         While 1             If $b[$i] = '>' Then                 $sChar = StringLeft($sString, 1)             Else                 $sChar = StringRight($sString, 1)             EndIf             For $i2 = 1 To $a[0]                 If StringCompare($a[$i2], $sChar, $iCaseSense) = 0 Then                     If $b[$i] = '>' Then                         $sString = StringTrimLeft($sString, 1)                         ContinueLoop 2                     Else                         $sString = StringTrimRight($sString, 1)                         ContinueLoop 2                     EndIf                 EndIf             Next             ExitLoop 1         WEnd     Next     Return $sString EndFunc   ;==>StringTrimPattern  Func _Print($sMsg) ;only used for demonstration purpose and clarity     ConsoleWrite($sMsg &amp; @CRLF) EndFunc   ;==>_Print
