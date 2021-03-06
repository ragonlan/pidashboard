# pidashboard
Grafana dasborad designed for Raspberry pi Systems

Based in Telegraf: system dashboardby Lex Rivera: https://grafana.com/grafana/dashboards/928

Telegraf config:
```
[[inputs.disk]]
  percpu = true
  totalcpu = true
  collect_cpu_time = false
  report_active = false
[[inputs.diskio]]
  device_tags = ["ID_FS_TYPE", "ID_FS_USAGE"]
  name_templates = ["$ID_FS_LABEL","$DM_VG_NAME/$DM_LV_NAME"]
[[inputs.kernel]]
[[inputs.mem]]
[[inputs.processes]]
[[inputs.swap]]
[[inputs.system]]
[[inputs.internal]]
[[inputs.interrupts]]
   cpu_as_tag = true
[[inputs.linux_sysctl_fs]]
[[inputs.net]]
[[inputs.netstat]]
[[inputs.nstat]]
[[inputs.file]]
  files = ["/sys/class/thermal/thermal_zone0/temp"]
  name_override = "cpu_temperature"
  data_format = "value"
  data_type = "integer"

[[inputs.exec]]
  commands = [ "/opt/vc/bin/vcgencmd measure_temp"]
  name_override = "gpu_temperature"
  data_format = "grok"
  grok_patterns = ["%{NUMBER:value:float}"]

[[inputs.exec]]
  commands = ["/opt/vc/bin/vcgencmd measure_clock arm"]
  name_override = "cpu_clock"
  data_format = "grok"
  grok_patterns = ["=%{NUMBER:value:float}"]

[[inputs.exec]]
  commands = [ "/opt/vc/bin/vcgencmd measure_volts core"]
  name_override = "volts"
  data_format = "grok"
  grok_patterns = ["%{NUMBER:value:float}"]
[[inputs.exec]]
  commands = [ "/opt/vc/bin/vcgencmd measure_volts sdram_c"]
  name_override = "volts"
  data_format = "grok"
  grok_patterns = ["%{NUMBER:sdramc:float}"]
[[inputs.exec]]
  commands = [ "/opt/vc/bin/vcgencmd measure_volts sdram_i"]
  name_override = "volts"
  data_format = "grok"
  grok_patterns = ["%{NUMBER:sdrami:float}"]
[[inputs.exec]]
  commands = [ "/opt/vc/bin/vcgencmd measure_volts sdram_p"]
  name_override = "volts"
  data_format = "grok"
  grok_patterns = ["%{NUMBER:sdramp:float}"]
[[inputs.exec]]
  commands = [ "python3 /media/pi/f9fb5995-3bd5-4ac0-859a-aa5bf467905d/opt/pidata/throttling.py"]
  name_override = "throttling"
  data_format = "json"
```
