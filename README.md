ey-cloud-recipes
===============
This is a repository of some basic recipes for EY-Cloud using chef to deploy, setup, and configure common tools for Rails applications.


Installation
============

Follow these steps to use custom deployment recipes with your applications.

* Install the engineyard gem:
  $ gem install engineyard
* Add any custom recipes or tweaks to your copy of these recipes.
* Upload them with: `ey recipes upload -e ENV`, where ENV is the name of your environment in Engine Yard Cloud. This may be different than your Rails environment name.
* Once you have completed these steps, each rebuild will run the your
  recipes after the default Engine Yard recipes have run. When you
  update your recipes, just re-run `ey recipes upload -e ENV`.


Notes
============

In case someone has problems on running delayed_jobs, there are several things you can look at:

* make sure there are monit processes running under /etc/monit.d and the file name should look like:
  delayed_jobNUM.APP_NAME.monitrc (ex. delayed_job1.coupondudes.monitrc)
* if not, then make sure you have modified 'cookbooks/delayed_job/recipes/default.rb' correctly, commit, and push the change. then execute these:
  ey recipes upload -e ENV
  ey recipes apply -e ENV
* in 'cookbooks/delayed_job/recipes/default.rb', make sure you include the right 'node[:instance_role]' at line 6.