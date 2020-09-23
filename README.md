<div align="center">

## Move/Add/Swap/Transfer Data Client Side


</div>

### Description

If you&#8217;ve ever had two multiple selection boxes, and wanted to transfer the values of the multiple selection boxes back and forth, then finally submit the code in the adjusted multiple selection box(s), here&#8217;s the code to do it!
 
### More Info
 
Add the script between your HEAD tags. Your items placed into the multiple selection box.

Modify only the code you need to, i.e., the form tag post to, the name of the two multiple selection boxes, and its title. If copied verbatim, there should be no side effects. Enjoy!


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Matt Khoury](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/matt-khoury.md)
**Level**          |Intermediate
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__2-68.md)
**World**          |[Java](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/java.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/matt-khoury-move-add-swap-transfer-data-client-side__2-2525/archive/master.zip)





### Source Code

```
<!doctype html public "-//W3C//DTD HTML 4.0 Transitional//EN">
<html>
<head>
	<title>Transfer Values Back & Forth</title>
<style type="text/css">
	TABLE	{
		BORDER-BOTTOM: 0px;
		BORDER-LEFT: 0px;
		BORDER-RIGHT: 0px;
		BORDER-TOP: 0px;
		FONT-FAMILY: tahoma,sans-serif;
		FONT-SIZE: 14px;
		FONT-WEIGHT: BOLD;
		COLOR: White;
	}
	.MSB	{
		BORDER-BOTTOM: 0px;
		BORDER-LEFT: 0px;
		BORDER-RIGHT: 0px;
		BORDER-TOP: 0px;
		FONT-FAMILY: tahoma,sans-serif;
		FONT-SIZE: 12px;
	}
	.Main	{
		BORDER-BOTTOM: 0px;
		BORDER-LEFT: 0px;
		BORDER-RIGHT: 0px;
		BORDER-TOP: 0px;
		FONT-FAMILY: tahoma,sans-serif;
		FONT-SIZE: 12px;
		COLOR: White;
	}
</style>
<script language="JavaScript">
<!--
var conAdd = 'Add';
var conRemove = 'Remove';
var delimiter = "|";
function MoveOption(f, From, To, action) {
 var eFrom = eval('f.msb' + From);
	var eTo = eval('f.msb' + To);
	var selection = eFrom.options.selectedIndex;
	var eAddContainer;
	var eRemoveContainer;
	if (action == conAdd) {
		eAddContainer = eval('f.htx' + conAdd + To);
		eRemoveContainer = eval('f.htx' + conRemove + To);
	}
	if (action == conRemove) {
		eAddContainer = eval('f.htx' + conRemove + From);
		eRemoveContainer = eval('f.htx' + conAdd + From);
	}
	if (selection == -1) {
		alert("Please select one or more users to move.");
	} else {
		eval('f.cmd' + action + '.disabled = true;');
		for (i = 0; i < eFrom.options.length; i++) {
			if(eFrom.options[i].selected) {
				var name = eFrom.options[i].text;
				var ID = eFrom.options[i].value;
				eFrom.options[i] = null;
				eTo.options[eTo.options.length] = new Option (name,ID);
				i = i - 1;
				var rep = new String('\\' + delimiter + ID + '\\' + delimiter + '');
				var repExp = new RegExp(rep);
				if (eRemoveContainer.value.match(repExp) == null) {
					eAddContainer.value = eAddContainer.value + ID + delimiter;
				} else {
					eRemoveContainer.value = eRemoveContainer.value.replace(repExp,delimiter);
				}
			}
		}
	}
}
function onChange_msbUserPool(f) {
	f.cmdAdd.disabled = (f.msbUserPool.selectedIndex == -1);
}
function onChange_msbAssignedUser(f) {
	f.cmdRemove.disabled = (f.msbAssignedUser.selectedIndex == -1);
}
-->
</script>
</head>
<body>
<form action="more_values.html" method="post" id="thisForm" name="thisForm">
<input type="hidden" name="htxAddAssignedUser" id="htxAddAssignedUser" value="|">
<input type="hidden" name="htxRemoveAssignedUser" id="htxRemoveAssignedUser" value="|">
<table width="600" border="1" bordercolor="#103052" cellspacing="0" cellpadding="0" align="center" bgcolor="#336699">
	<tr>
		<td>
			<table border="0" bordercolor="red" cellspacing="0" cellpadding="3" align="center" width="100%">
				<tr>
					<td height="5" colspan="3"/>
				</tr>
				<tr class="main">
					<td colspan="3">Click on a member or members of Team One and then click Assign, or click on a member of Team Two, and click remove to assign back to Team One.</td>
				</tr>
				<tr>
					<td height="5" colspan="3"/>
				</tr>
				<tr>
					<td valign="top" width="50%">
						<table border="1" cellspacing="0" cellpadding="0" class="main" align="center" bordercolor="#103052">
							<tr>
								<td valign="middle" id="lblUserPool" bgcolor="#103052" nowrap> Team One: </td>
							</tr>
							<tr>
								<td valign='top' align="center">
									<select multiple size='20' id='msbUserPool' name='Unassigned User Pool' class='msb' onchange='onChange_msbUserPool(thisForm);'>
										<option value="1">Smith, John</option>
										<option value="2">Smith1, John</option>
										<option value="3">Smith2, John</option>
										<option value="4">Smith3, John</option>
										<option value="5">Smith4, John</option>
										<option value="6">Smith5, John</option>
									</select>
								</td>
							</tr>
						</table>
					</td>
					<td>
						<table border="0" cellspacing="0" cellpadding="0" class="main" align="center" bordercolor="red" width="100%">
							<tr>
								<td align="center"><input disabled onclick="MoveOption(thisForm,'UserPool','AssignedUser','Add');" type="button" value="Move >>" name="Assign User" id="cmdAdd" class="fbbutton"></td>
							</tr>
							<tr>
								<td height="25"/>
							</tr>
							<tr>
								<td align="center"><input disabled onclick="MoveOption(thisForm,'AssignedUser','UserPool','Remove');" type="button" value="<< Move" name="Remove User" id="cmdRemove" class="fbbutton"></td>
							</tr>
						</table>
					</td>
					<td valign="top" width="50%" align="center">
						<table border="1" cellspacing="0" cellpadding="0" class="main" bordercolor="#103052">
							<tr bgcolor="#103052">
								<td valign="middle" id="lblAssignedUser" nowrap> Team Two: </td>
							</tr>
							<tr>
								<td valign="middle" align="center">
									<select multiple size="20" id="msbAssignedUser" name="Assigned Users" class="msb" onchange="onChange_msbAssignedUser(thisForm);">
										<option value="1">Smith, Jane</option>
										<option value="2">Smith1, Jane</option>
										<option value="3">Smith2, Jane</option>
										<option value="4">Smith3, Jane</option>
										<option value="5">Smith4, Jane</option>
										<option value="6">Smith5, Jane</option>
									</select>
								</td>
							</tr>
						</table>
					</td>
				</tr>
				<tr>
					<td height="15" colspan="3"/>
				</tr>
				<tr>
					<td valign="top" align="center" colspan="3">
						<table border="0" cellspacing="0" cellpadding="0" class="main">
							<tr>
								<td><input type="submit" value="Submit Updates" id="cmdSubmit" name="Submit Updates"></td>
								<td width="15"></td>
								<td><input type="button" value="Reset" id="cmdReset" name="Reset" onClick="location.reload(true);"></td>
							</tr>
						</table>
					</td>
				</tr>
				<tr>
					<td height="15" colspan="3"/>
				</tr>
			</table>
		</td>
	</tr>
</table>
</form>
</body>
</html>
```

