<script src="../../jquery.min.js"></script>
<script src="../../qrcodeborder.js"></script>
<style>
        #qrcode{
            width: 100%;
        }
        div{
            width: 100%;
            display: inline-block;
        }
</style>

# Chapters Size Control

GoPro cameras normally split long recordings into 4GB segments, we call these chapters. These 4GB (32-bit) MP4 files are the most compatible, yet larger 64-bit MP4 files are becoming more common. Increase your chapter size to 12GB with this control below. 

<input type="checkbox" id="lchptrs" name="lchptrs" checked> 
<label for="lchptrs">Enable Large Chapters</label><br>
<center>
<div id="qrcode"></div>
<br>
</center>
QR Command: <b id="qrtext">command</b><br>

Warning: Larger chapters may not work everywhere in the ecosystem, even the camera will not playback files larger than 4GB in this current firmware. Yet the files are valid, and have been tested to work in many tools. So this one of the more experimental features, so please test before commiting to this new workflow.

<br> 
        
## ver 1.00
[BACK](..)

<script>
var once = true;
var qrcode;
var cmd = "";

function makeQR() 
{	
  if(once === true)
  {
    qrcode = new QRCode(document.getElementById("qrcode"), 
    {
      text : "!M64BT=1",
      width : 360,
      height : 360,
      correctLevel : QRCode.CorrectLevel.M
    });
    once = false;
  }
}

function timeLoop()
{
  cmd = "!M64BT=0";
  if(document.getElementById("lchptrs") !== null)
  {
    if(document.getElementById("lchptrs").checked === true)
    {
      cmd = "!M64BT=1";
    }
  }

  qrcode.clear(); 
  qrcode.makeCode(cmd);
  document.getElementById("qrtext").innerHTML = cmd;
  var t = setTimeout(timeLoop, 50);
}

function myReloadFunction() {
  location.reload();
}

makeQR();
timeLoop();

</script>
