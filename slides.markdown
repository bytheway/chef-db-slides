%css

body {
  background-image: -webkit-linear-gradient(top, #003399, #000099);
  background-image:    -moz-linear-gradient(top, #003399, #000099);
  background-image:     -ms-linear-gradient(top, #003399, #000099);
  background-image:      -o-linear-gradient(top, #003399, #000099);
  background-image:         linear-gradient(top, #003399, #000099);

  font-family: 'Monda', sans-serif;
}


.step {
  width: 900px;
  height: 420px;
  display: block;
  transition: opacity 1s;
}

.step.active {
  opacity: 1;
}

.step:not(.active) {
      opacity: 0;
}


.chef {
  min-width: 400px;
  min-height: 400px;
  padding: 40px 60px;

  font-size: 48px;
  text-align: center;

  color: white;
  opacity: 0.3;
  #background-color: white;
}


.chef.step {
  width: 900px;
  height: 420px;
  display: block;
  transition: opacity 1s;
}

.chef.step.active {
  opacity: 1;
}

.chef.step:not(.active) {
      opacity: 0.5;
}

.slide {
  min-width: 1000px;
  min-height: 600px;
  padding: 40px 60px;

  font-size: 48px;
  text-align: center;

  opacity: 0.3;
  background-color: white;
}

.slide-center {
  display: table-cell;
  min-width: 1000px;
  min-height: 600px;
  padding: 40px 60px;

  font-size: 48px;
  text-align: center;

  opacity: 0.3;
  background-color: white;
}
ul {
  text-align: left;
  font-size: 38px;
  line-height: 70px;
}

pre, code {
  font-size: 32px;
  line-height: 38px;
  margin-left: 30px;
  text-align: left;
}

%end

!SLIDE slide-center
<link href='http://fonts.googleapis.com/css?family=Monda:400,700' rel='stylesheet' type='text/css'>
Just enough Chef to make your head hurt

<img src="images/chef-logo.png" style="max-height: 300px; max-width=800px;">

!SLIDE slide x=1200

What is Chef?

* Provisioner
* Configuration Management
* Configuration as code

!SLIDE slide x=2400

Configuration as Code

* Check your configuration into source control
* Test your configuration before rolling it out

!SLIDE slide x=0 y=1000

Idempotent

* Run configuration manager multiple times, results always the same
* Only things that need to change are changed
* Kind of like:
<% code do %>
CREATE OR REPLACE PROCEDURE MyProcedure
...
<% end %>

!SLIDE chef x=0 y=-1000

![](images/uparrow.png)

Resources

!SLIDE chef x=0 y=-1300

![](images/uparrow.png)

Recipes

!SLIDE chef x=0 y=-1600

![](images/uparrow.png)

Cookbooks

!SLIDE chef x=0 y=-1762

Roles

!SLIDE chef x=300 y=-1762

Nodes

!SLIDE slide x=1200 y=1000

Recipes

* Collections of Resources
* Declarative.
* Tell **what** you want, not **how**

<% code do %>
directory '/opt/oracle' do
  owner 'oracle'
  mode '0755'
end
<% end %>

!SLIDE slide x=2400 y=1000

Resources

* Basic building block
* Files, directories, packages (rpm), templates, cron jobs, users, groups, scripts

!SLIDE slide x=0 y=2000

<p style="margin-top: 200px;">
  How might a DBA use it?
</p>

!SLIDE slide x=1200 y=2000

Install Oracle Dependencies

<% code do %>
for rpm in ['binutils', 'compat-libcap1', 
            'compat-libstdc++-33', 'gcc',  
            'gcc-c++', 'glibc', 'glibc-devel', 
            'ksh', 'libgcc', 'libstdc++', 
            'libstdc++-devel', 'libaio', 
            'libaio-devel', 'make', 'sysstat']
  package rpm
end
<% end %>

!SLIDE slide x=2400 y=2000

Users and Groups

<% left do %>
<% code do %>
group 'dba' do
  gid 500
end


user 'oracle' do
  uid 600
  gid 'dba'
end
<% end %>
<% end %>

<% right do %>
<% code do %>
group 'oinstall' do
  gid 501
  members 'oracle'
end

group 'oper' do
  gid 502
  members 'oracle'
end
<% end %>
<% end %>

!SLIDE slide x=3600 y=2000

Directories

<% code do %>
  directory '/u01/app/oracle/product/10.2.0/db_1' do
    owner 'oracle'
    group 'oinstall'
    mode '0755'
    recursive true
  end
<% end %>

!SLIDE slide x=4800 y=2000

And so on...

* Install oracle itself
* Manage basic authentication / passowrds
* Create databases
* Setup backups

!SLIDE slide x=6000 y=2000

Community Cookbooks, too

* Just released an Oracle/RHEL install cookbook
* https://github.com/echaeu/echa-oracle/
