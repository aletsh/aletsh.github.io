---
id: 69
title: 'PyroCMS SQLSTATE[HY000] [2002] No such file or directory'
date: 2017-11-28T17:55:16+00:00
author: aletsh
layout: post
guid: http://alejandroguerrero.es/2017/11/28/pyrocms-sqlstatehy000-2002-no-such-file-or-directory/
permalink: /pyrocms-sqlstatehy000-2002-no-such-file-or-directory/
categories:
  - Uncategorized
tags:
  - pyrocms
  - 'SQLSTATE[HY000]'
---
Si estas empleando MAMP/MAMP PRO y tienes un error de este tipo al crear un addon / plantilla etc, osea con este comando:

<span class="s1">php artisan make:addon example.theme.demo</span>

Y te deveulve lo siguiente:

 <span class="s1">[IlluminateDatabaseQueryException]<span class="Apple-converted-space">                                         </span></span><span class="s1"><span class="Apple-converted-space">  </span>SQLSTATE[HY000] [2002] No such file or directory (SQL: select * from <code>my_new_project &lt;/span&gt;&lt;span class="s1"&gt;_settings_settings</code>)<span class="Apple-converted-space">                                                   </span></span><span class="s1"><span class="Apple-converted-space">  </span>[DoctrineDBALDriverPDOException]<span class="Apple-converted-space">               </span></span><span class="s1"><span class="Apple-converted-space">  </span>SQLSTATE[HY000] [2002] No such file or directory </span><span class="s1"><span class="Apple-converted-space">                                       </span></span><span class="s1"><span class="Apple-converted-space">  </span>[PDOException] <span class="Apple-converted-space">                                   </span></span><span class="s1"><span class="Apple-converted-space">  </span>SQLSTATE[HY000] [2002] No such file or directory </span>

Tienes que indicarle a la configuración local de tu proyecto PyroCMS que necesitas emplear el socket de Mysql del MAMP en: /config/database.php

<div>
  &#8216;mysql&#8217; => [ &#8230; &#8216;unix_socket&#8217; => &#8216;/Applications/MAMP/tmp/mysql/mysql.sock&#8217;, &#8230; ],
</div>

<div>
   ![](/content/images/2017/05/Captura-de-pantalla-2017-05-15-a-las-19.55.20.png)
</div>

<div>
  Enjoy!
</div>