# Default

<h1>Horizon: Geeklog 2.1.1 Default Geeklog Theme</h1>

<p>Geeklog theme using HTML5 + CSS 3.0 + CSS Frontend framework UIkit and eliminate table tags.<br>
This theme is adopted the Responsive Web Design.<br>
This theme is mobile friendly.</p>

<p>Copyright (C) 2012-2015 by the following authors:<br>
<br>
Author: <br>
Tetsuko Komma - http://www.ivywe.co.jp/<br>
<br>
Original Author: <br>
Fumito Arakawa   - http://phize.net/ <br>
Geeklog Japan    - http://www.geeklog.jp/ <br>
Yoshinori Tahara - taharaxp AT gmail DOT com<br>
<br>
style.css.php Author: <br>
Authors: Rouslan Placella  - rouslan@placella.com<br>
</p>

<p>UIkit: CSS Frontend framework<br>
http://getuikit.com/</p>


<p>This program is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License
as published by the Free Software Foundation; either version 2
of the License, or (at your option) any later version.</p>
                                 
<p>This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.</p>
                                 
<p>You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software Foundation,
Inc., 59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.</p>
                                 
<h2>Basic Markup</h2>

<p>Basic markup is following:</p>

<pre>
&#60;div id="container"&#62;
    &#60;header id="header"&#62;Header&#60;/header&#62;
    &#60;nav id="navigation"&#62;Navigation&#60;/nav&#62;
    &#60;div id="wrapper"&#62;
        &#60;div id="centerblocks"&#62;
            &#60;main id="main-content"&#62;Main Content&#60;/main&#62;
        &#60;/div&#62;
        &#60;div id="leftblocks"&#62;Left Blocks&#60;/div&#62;
        &#60;div id="rightblocks"&#62;Right Blocks&#60;/div&#62;
    &#60;/div&#62;
    &#60;footer id="footer"&#62;Footer&#60;/footer&#62;
&#60;/div&#62;
</pre>



<p>hack system/lib-comment.php</p>

<pre>
@@ -412,7 +412,7 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals

        // this will hide HTML that should not be viewed in preview mode
        if( $preview || $hidefromanon ) {
            $template->set_var( 'hide_if_preview', 'style="display:none"' );
            $template->set_var( 'hide_if_preview', ' style="display:none"' );
        } else {
            $template->set_var( 'hide_if_preview', '' );
        }
@@ -432,7 +432,7 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals
                       . '&amp;order=' . $order . '&amp;cid=' . $A['pid']
                       . '&amp;format=threaded';
            }
            $parent_link = COM_createLink($LANG01[44], $plink) . ' | ';
            $parent_link = COM_createLink($LANG01[44], $plink) ;
            $template->set_var('parent_link', $parent_link);
        } else {
            $template->set_var('parent_link', '');
@@ -475,7 +475,7 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals
                $editlink = $_CONF['site_url'] . '/comment.php?mode=edit&amp;cid='
                    . $A['cid'] . '&amp;sid=' . $A['sid'] . '&amp;type=' . $type;
            }
            $edit = COM_createLink($LANG01[4], $editlink) . ' | ';
            $edit = COM_createLink($LANG01[4], $editlink) ;
        }

        // unsubscribe link
@@ -495,7 +495,7 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals
                }
                $unsubattr = array('title' => $LANG03[43]);
                $unsubscribe = COM_createLink($LANG03[42], $unsublink,
                                              $unsubattr) . ' | ';
                                              $unsubattr) ;
            }
        }

@@ -505,7 +505,7 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals

            // always place edit option first, if available
            if (! empty($edit)) {
                $deloption .= $edit;
                $deloption .= "<li>".$edit."</li>";
            }

            // actual delete option
@@ -519,15 +519,15 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals
                    . '&amp;' . CSRF_TOKEN . '=' . $token;
            }
            $delattr = array('onclick' => "return confirm('{$MESSAGE[76]}');");
            $deloption .= COM_createLink($LANG01[28], $dellink, $delattr) . ' | ';
            $deloption .= "<li>".COM_createLink($LANG01[28], $dellink, $delattr)."</li>" ;

            if (!empty($A['ipaddress'])) {
                if (empty($_CONF['ip_lookup'])) {
                    $deloption .= $A['ipaddress'] . '  | ';
                    $deloption .= "<li>".$A['ipaddress']."</li>";
                } else {
                    $iplookup = str_replace('*', $A['ipaddress'],
                                            $_CONF['ip_lookup']);
                    $deloption .= COM_createLink($A['ipaddress'], $iplookup) . ' | ';
                    $deloption .= "<li>".COM_createLink($A['ipaddress'], $iplookup)."</li>";
                }
            }

@@ -551,7 +551,7 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals
                }
                $report_attr = array('title' => $LANG01[110]);
                $reportthis = COM_createLink($LANG01[109], $reportthis_link,
                                             $report_attr) . ' | ';
                                             $report_attr) ;
            }
            $template->set_var('delete_option', $reportthis . $unsubscribe);
        } else {
@@ -597,7 +597,7 @@ function CMT_getComment( &$comments, $mode, $type, $order, $delete_option = fals
                            . '&amp;pid=' . $A['cid'] . '&amp;type=' . $A['type'];
            }
            $reply_option = COM_createLink($LANG01[43], $reply_link,
                                           array('rel' => 'nofollow')) . ' | ';
                                           array('rel' => 'nofollow'));
            $template->set_var('reply_option', $reply_option);
        } else {
            $template->set_var('reply_option', '');

</pre>
