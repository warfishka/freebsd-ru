 ___       __         ______________        _____
 __ |     / /___________  ____/__  /_______ __  /_
 __ | /| / /_  _ \  _ \  /    __  __ \  __ `/  __/
 __ |/ |/ / /  __/  __/ /___  _  / / / /_/ // /_
 ____/|__/  \___/\___/\____/  /_/ /_/\__,_/ \__/
 
WeeChat 1.3 [compiled on Aug 17 2015 07:51:18]

# Installation
## CYGWIN

## Babun
babun update
pact install weechat weechat-python weechat-python weechat-perl weechat-tcl weechat-ruby weechat-lua aspell asplell-en

## Linux
sudo apt-get update && apt-get upgrade
sudo apt-get install weechat weechat-plugins


# Configuration
## Encrypted password in sec.conf
/secure passphrase <pass>

## Default setting for all network
/set irc.server_default.nicks lanbird
/set irc.server_default.ssl_verify off


# Setting for networks
## Bitlbee
/server add BitlBee 192.168.1.133/6667 -autoconnect
/set irc.server.BitlBee.command "/query root identify c66g2wksqa"
# /set irc.server.BitlBee.command "/exec -norc -buffer conky true"

## bitlbee twitter (you need to add them before joining)
/msg -server BitlBee root chat add twitter follow:lanbird;follow:0x600 #lanbird
/msg -server BitlBee root channel #lanbird set auto_join true
/join -server BitlBee #lanbird

## irc
/server del freenode
/server add freenode freenode.com/6667 -ssl -autoconnect
/set irc.server.freenode.password <pass>

## bnc
/secure set bncpass <pass>
/set irc.server_default.capabilities "znc.in/server-time-iso"
/server add freenode znc.pascalpoitras.com/30011 -ssl -autoconnect
/set irc.server.freenode.password r3m/freenode:${sec.data.bncpass}


# Extensions
## Autoload
/set weechat.plugin.autoload "*,!lua,!tcl,!ruby,!fifo,!logger,!relay"

# Scripts
/script install buffers.pl text_item.py notify.py translate.py highmon.pl buffer_autoset.py urlserver.py iset.pl cmd_help.py perlexec.pl autosort.py

## aspell
/set aspell.check.default_dict fr
/set aspell.check.suggestions 3
/set aspell.color.suggestions *green
/allchan -exclude=*fr aspell setdict en
/buffer &france
/allchan -current aspell setdict fr
/aspell enable

## xfer
/set xfer.network.port_range 10051-10070

## translate.py
/set plugins.var.python.translate.default "ru_fr"

## highmon.pl
/set plugins.var.perl.highmon.alignment "nchannel"

## buffer_autoset.py
# /autosetbuffer add exec.exec.conky title System monitor
/autosetbuffer add irc.BitlBee.&france title France: General Account [anonym]
/autosetbuffer add irc.Freenode.* filter 0
/autosetbuffer add irc.Freenode.#mychan short_name <shortname>

## cmd_help.py
/key bind meta-OP /cmd_help

## urlserver.py
/set plugins.var.python.urlserver.http_hostname "127.0.0.1"
/set plugins.var.python.urlserver.http_port 3113
/set plugins.var.python.urlserver.http_allowed_ips "^127.0.0.1$"
/set plugins.var.python.urlserver.http_url_prefix url
/set plugins.var.python.urlserver.msg_ignore_buffers core.weechat,python.grep,perl.highmon
/set plugins.var.python.urlserver.msg_ignore_buffers irc.BitlBee.#twitter_lanbird,irc.freenode.##news

## iset.pl
/set iset.color.bg_selected 29
/set iset.color.option_selected white
/set iset.color.value_selected *white
/set iset.color.value 121


!!!## pushover.pl
//set plugins.var.perl.pushover.service pushbullet
//set plugins.var.perl.pushover.pb_apikey <the apikey>
//set plugins.var.perl.pushover.blacklist *status,xfer.irc_dcc.UnderNet.ReeBot


!!!# Layouts

## Layout news (5x windows)
/window splith 50
/buffer #twitter_pascalpoitras
/window splitv 92
/buffer &facebook
/window 2
/window splith 66
/buffer irc.BitlBee.#quebec
/window splith 50
/buffer highmon
/window 1
/layout store news


!!!## Layout news-conky
/window splitv 78
/buffer exec.conky
/layout store news-conky


!!# Customize the nicklist bar
/set weechat.bar.nicklist.color_fg 229
/set weechat.bar.nicklist.separator on
/set weechat.bar.nicklist.conditions "${nicklist} && ${window.number} == 1"
/window 3
/eval /set weechat.bar.nicklist.size_max ${window.win_width}
/eval /set weechat.bar.nicklist.size ${window.win_width}
/window 1


!!# Create and customize the nicklistfb bar


/bar add nicklistfb window left 12 0 buffer_nicklist
/set weechat.bar.nicklistfb.color_fg 229
/set weechat.bar.nicklistfb.separator on
/window 3
/eval /set weechat.bar.nicklistfb.size_max ${window.win_width}
/eval /set weechat.bar.nicklistfb.size ${window.win_width}
/set weechat.bar.nicklistfb.size --1
/window 1
/set weechat.bar.nicklistfb.size 0
/set weechat.bar.nicklistfb.size_max 0
/set weechat.bar.nicklistfb.conditions "${window.number} == 3 && ${channel} == &facebook"


!!!# Customize the buffers bar
## unmerge servers buffers from core and indent
/set irc.look.server_buffer independent
/set buffers.look.indenting on

## main color scheme
/set buffers.color.current_fg white
/set buffers.color.current_bg 29
/set buffers.color.hotlist_message_fg 229
/set buffers.color.hotlist_private_fg 121
/set buffers.color.hotlist_highlight_fg red


!!## whitelist color scheme
/set buffers.look.whitelist_buffers "server.UnderNet,server.TripSit,server.OFTC,server.NetChat,server.freenode,server.EFNet,server.DivinityCoding,server.DaIRC,server.BitlBee,server.EvoluNET"
/set buffers.color.whitelist_default_bg 31
/set buffers.color.whitelist_highlight_bg 31
/set buffers.color.whitelist_low_bg 31
/set buffers.color.whitelist_message_bg 31
/set buffers.color.whitelist_private_bg 31
/set buffers.color.whitelist_highlight_fg 198
/set buffers.color.whitelist_message_fg 221
/set buffers.color.whitelist_private_fg 83


!!## buffers
/set weechat.bar.buffers.size_max 14
/set buffers.color.number 239
/set buffers.color.number_char 245


# Create and customize activetitle bar
/bar add activetitle window top 1 0 buffer_title
/set weechat.bar.activetitle.priority 500
/set weechat.bar.activetitle.conditions "${active}"
/set weechat.bar.activetitle.color_fg *white
/set weechat.bar.activetitle.color_bg 31

# inactive title bar
/set weechat.bar.title.conditions "${inactive}"
/set weechat.bar.title.color_fg 31
/set weechat.bar.title.color_bg 233


# Create and customize the rootstatus bar
/bar add rootstatus root bottom 1 0 [time],[buffer_count],[buffer_plugin],buffer_number+:+buffer_name+(buffer_modes)+{buffer_nicklist_count}+buffer_filter,[bitlbee_typing_notice],[lag],[aspell_suggest],[hotlist],completion,scroll
/set weechat.bar.rootstatus.color_fg red
/set weechat.bar.rootstatus.separator on
/set weechat.bar.rootstatus.priority 500
/bar del status
/bar set rootstatus name status


# Create and customize the rootinput bar
/bar add rootinput root bottom 1 0 [buffer_name]+[input_prompt]+(away),[input_search],[input_paste],input_text
/set weechat.bar.rootinput.priority 1000
/bar del input
/bar set rootinput name input


# Create and customize the roottranslation bar
/bar add roottranslation root top 1 0 [translation_desc],[translation_text]
/set weechat.bar.roottranslation.color_fg 31
/set weechat.bar.roottranslation.color_bg black
/set weechat.bar.roottranslation.separator on
/set plugins.var.python.text_item.translation_desc all ${121}Translation
/set plugins.var.python.text_item.translation_text all Press 't' in cursor mode to translate the text under the cursor and make it appears here. Then, the text will dissapears 10 seconds later. To enter cursor mode : middle-mouse button
/key bindctxt cursor @chat:t /input delete_line;/input insert /translate en_fr\x20;hsignal:chat_quote_message;/input return;/wait 1 /input move_beginning_of_line;/wait 1 /input insert /set plugins.var.python.text_item.translation_text all\x20;/wait 1 /input return;/cursor stop;/wait 10 /set plugins.var.python.text_item.translation_text all Press 't' in cursor mode to translate the text under the cursor and make it appears here. Then, the text will dissapears 10 seconds later. To enter cursor mode : middle-mouse button




# Highlight
/set weechat.look.highlight_regex .*lanbird.*
/autosetbuffer add irc.BitlBee.#twitter_lanbird* highlight_regex .*weechat.*
/autosetbuffer add irc.BitlBee.#twitter_lanbird* highlight_words tor,hack,nsa
/autosetbuffer add irc.BitlBee.#lanbird highlight_regex .*
/autosetbuffer add irc.freenode.##news highlight_regex .*weechat.*
/autosetbuffer add irc.freenode.##news highlight_words tor
//autosetbuffer add irc.freenode.##reddit-hockey highlight_regex (^GOAL: MTL.*|^Le But: MTL.*)


# Triggers


/trigger addreplace beep_highlight print "" "${tg_highlight}" "" "/exec -bg beep -f 500 -r 2" "ok"
/trigger addreplace beep_pv print "" "${tg_msg_pv}" "" "/exec -bg beep -f 3000 -r 3" "ok"
/trigger addreplace beep_notify_join signal irc_notify_join "" "/.*\,//" "/exec -bg beep -f 4000 -r 1;/exec -bg notify-send -i /usr/share/pixmaps/weechat.xpm '${tg_signal_data}' 'is online'" "ok"
/trigger addreplace beep_notify_quit signal irc_notify_quit "" "/.*\,//" "/exec -bg beep -f 4500 -r 1;/exec -bg notify-send -i /usr/share/pixmaps/weechat.xpm '${tg_signal_data}' 'is offline'" "ok"
/trigger addreplace url_color modifier weechat_print "${tg_notify}" "==\S+://\S+==${color:*white}${re:0}${color:reset}==" ""
/trigger addreplace hockeygoal signal freenode,irc_in_privmsg "${nick} == GoalBot && ${tg_signal_data} =~ (Le But|Goal|Scoring Change).*\s(MTL|OTT)\s" "/(.*):(.*):(.*):(.*)/${re:2}:${re:3}:${re:4}/arguments" "/msg -server UnderNet #nullepart ${arguments}" "ok"
/trigger addreplace habsgame signal freenode,irc_in_privmsg "${nick} == GoalBot && ${tg_signal_data} =~ \sMontreal\s" "/(.*):(.*)/${re:2}/arguments" "/msg -server UnderNet #nullepart ${arguments}" "ok"
/trigger addreplace window_6_hidden_kill_conky signal window_zoom "${window[${tg_signal_data}].number} != 6" "" "/exec -bg killall conky" "ok"
/trigger addreplace window_6_not_hidden_launch_conky signal window_unzoom "${window[${tg_signal_data}].number} != 6" "" "/exec -bg conky" "ok"
/trigger addreplace upgrade_scripts signal day_changed "" "" "/script update;/wait 10s /script upgrade" "ok"
/trigger addreplace quakenet_undernet_pm signal quakenet,irc_in_privmsg;UnderNet,irc_in_privmsg "${host} !~ (users.quakenet.org|users.undernet.org|znc@znc.in) && ${channel} == ${info:irc_nick,${server}}" "" "/msg -server ${server} ${nick} Please set the umode +x to chat with me. You are now silenced.;/quote -server ${server} silence +${host}" "ok"
/trigger addreplace disconnected_text modifier weechat_print "${tg_buffer} =~ irc.BitlBee.&facebook && ${tg_message} =~ disconnected from server" "/.*//" ""
/trigger addreplace keep_nick signal "irc_notify_quit" "${tg_signal_data} == UnderNet,stallman" "" "/command -buffer irc.server.UnderNet irc /nick Stallman" "ok"


# Keys


/key bindctxt cursor @item(buffer_nicklist):v /window ${_window_number};/voice ${nick}
/key bindctxt cursor @item(buffer_nicklist):o /window ${_window_number};/op ${nick}
/key bindctxt cursor @item(buffer_nicklist):V /window ${_window_number};/devoice ${nick}
/key bindctxt cursor @item(buffer_nicklist):O /window ${_window_number};/deop ${nick}
/key bindctxt cursor @item(buffer_nicklist):s /window ${_window_number};/me slaps ${nick} around a bit with a large trout
/key bindctxt cursor @item(buffer_nicklist):f /window ${_window_number};/trigger add female_${nick} modifier weechat_print "\${tg_tags} =~ ,irc_privmsg, && \${tg_tag_nick} == ${nick} && \${tg_buffer} !~ perl.highmon" "/(.*)/\${tg_prefix}\t\${color:219}\${tg_message}/" "";/cursor stop
/key bindctxt cursor @item(buffer_nicklist):m /window ${_window_number};/trigger add male_${nick} modifier weechat_print "\${tg_tags} =~ ,irc_privmsg, && \${tg_tag_nick} == ${nick} && \${tg_buffer} !~ perl.highmon" "/(.*)/\${tg_prefix}\t\${color:45}\${tg_message}/" "";/cursor stop
/key bindctxt cursor @item(buffer_nicklist):r /window ${_window_number};/trigger add bot_${nick} modifier weechat_print "\${tg_tags} =~ ,irc_privmsg, && \${tg_tag_nick} == ${nick} && \${tg_buffer} !~ perl.highmon" "/(.*)/\${tg_prefix}\t\${color:208}\${tg_message_nocolor}/" "";/cursor stop
/key bindctxt cursor @item(buffer_nicklist):B /window ${_window_number};/who ${chan};/wait 2s /perlexec my $infolist=weechat::infolist_get("irc_nick", "", '${server},${channel},${nick}')\;weechat::infolist_next($infolist)\;my $hostname = (split("@", weechat::infolist_string($infolist, "host")))[1]\;weechat::command("", ('${server}' eq "UnderNet") ? '/msg -server ${server} x@channels.undernet.org ban ${channel} *!*@' . $hostname . ' 100d 300 bye bye' : '/msg -server ${server} chanserv@services. akick ${channel} add *!*@' . $hostname . ' !P bye bye | Default ban');/cursor stop
/key bindctxt mouse @item(buffer_nicklist):button1 /window 1;/query ${nick}
/key bindctxt cursor @item(buffers):h /command -buffer ${full_name} irc /allchan -current buffer hide;/command -buffer ${full_name} irc /allpv -current buffer hide;/cursor stop
/key bindctxt cursor @item(buffers):H /command -buffer ${full_name} irc /allchan -current buffer unhide;/command -buffer ${full_name} irc /allpv -current buffer unhide;/cursor stop


# Others Keyboard shortcuts


/key bind meta-meta2-A /bar scroll nicklist * -100%
/key bind meta-meta2-B /bar scroll nicklist * +100%
/key bind meta2-A /input history_global_previous
/key bind meta2-B /input history_global_next


# Alias


/alias add cq allpv /buffer close
/alias add fr2en /translate
/alias add en2fr /translate !
/alias add beepoff /trigger disable beep;/trigger disable beep_highlight;/trigger disable beep_pv;/trigger disable beep_notify_join;/trigger disable beep_notify_quit;/trigger
/alias add beepon /trigger enable beep;/trigger enable beep_highlight;/trigger enable beep_pv;/trigger enable beep_notify_join;/trigger enable beep_notify_quit;/trigger
/alias add slap /me slaps $1 around a bit with a large trout
/alias add silence_pm /trigger toggle quakenet_undernet_pm;/allserv quote silence -*


# Filters


/set irc.look.smart_filter on
/filter add irc_smart * irc_smart_filter *
/filter add rt irc.BitlBee.#quebec * ^\[.*\]\sRT\s


# The remaining IRC options


/set irc.server_default.away_check 5
/set irc.server_default.away_check_max_nicks 25
/set irc.color.nick_prefixes "q:lightred;a:lightcyan;o:121;h:lightmagenta;v:229;*:lightblue"
/set irc.network.ban_mask_default "*!*@$host"


# Buffers notify level


/allserv set weechat.notify.irc.$server.*status none


# The remaining Weechat options


/set weechat.look.bar_more_down "▼"
/set weechat.look.bar_more_left "◀"
/set weechat.look.bar_more_right "▶"
/set weechat.look.bar_more_up "▲"
/set weechat.look.buffer_time_format "${253}%H${245}%M"
/set weechat.look.color_inactive_message off
/set weechat.look.color_inactive_prefix off
/set weechat.look.color_inactive_prefix_buffer off
/set weechat.look.color_inactive_window off
/set weechat.look.day_change_message_1date ▬▬▶ %a, %d %b %Y ◀▬▬
/set weechat.look.day_change_message_2dates ▬▬▶ %%a, %%d %%b %%Y (%a, %d %b %Y) ◀▬▬
/set weechat.look.hotlist_count_max 0
/set weechat.look.hotlist_names_count 10
/set weechat.look.item_buffer_filter "•"
/set weechat.look.prefix_align_min 10
/set weechat.look.prefix_align_max 10
/set weechat.look.prefix_join "▬▬▶"
/set weechat.look.prefix_quit "◀▬▬"
/set weechat.look.prefix_suffix "│"
/set weechat.look.read_marker_string "─"
/set weechat.look.separator_horizontal "="

/set weechat.color.bar_more 229
/set weechat.color.chat_highlight lightred
/set weechat.color.chat_highlight_bg default
/set weechat.color.chat_nick_colors 25,31,37,43,49,61,67,73,79,85,97,103,109,115,121,133,139,145,151,157,163,169,175,181,187,193,199,205,211,217,223,229
/set weechat.color.chat_prefix_join 121
/set weechat.color.chat_prefix_more 229
/set weechat.color.chat_prefix_quit 163
/set weechat.color.chat_prefix_suffix 31
/set weechat.color.chat_read_marker 31
/set weechat.color.chat_time 239
/set weechat.color.chat_delimiters 31
/set weechat.color.separator 31
/set weechat.color.status_data_highlight 163
/set weechat.color.status_data_msg 229
/set weechat.color.status_data_private 121
/set weechat.color.status_more 229
/set weechat.color.status_name 121
/set weechat.color.status_name_ssl 121
