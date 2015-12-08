ImproTessellate
--------------------------------------------------------------------------------

This project is being designed to help oneself become a more well-rounded
individual. What's more well-rounded than a sphere? What's a good way to 
do make somethings? One small bit a time, of course. How would one plan
on creating a spherical shape consisting of small, roughly uniform portions?
Tessellation!  


# Brainstorming

* ## Facets — One area to improve
  * Can be recurring (daily, weekly), a one-off of import (ex: oil change,
    doctor appointment), or whatever ad-hoc schedule/parameters you wish
  * Important to keep the goals small as possible
    * Once people do a bunch of little small things, they're likely to
      run out of easy ideas, or get more bold.
    * Either way, people will naturally try more meaningful changes over
      enough time
* ## Example facets of improvement 
  * Keep kitchen sink (daily)
  * Empty bathroom trash can immediately once it's over 3/4 full
  * Vacuum (weekly)
  * Make sure all bills are paid (weekly)
  * Wake up on weekends by 10:00
  * Go to bed by midnight weekdays
  * Don't go out on pay days
  * Brush teeth every morning
  * Brush teeth every night
  * Take any prescribed medication
  * Open mail immediately when getting home
  * Clean out kitty litter
  * 30 minutes of exercise N times per week
  * N pushups and M crunches daily
* ## Important Screens
  * A page to show the current goal for this week
    * previous weeks in a list below (limited to N most recent unless
      user choses to expand it)
  * Daily Log page
    * Lists the current and all previous (recurring) facets
    * Button bar/group
      * Completed
      * Not yet (disabled on daily facets)
      * Missed (better than writing *failure* `;-)`)
      * Add Note
  * Calendar view of old daily logs
    * color coded to show days with 100% success logs, partial success,
      days of failure, and days without a record
  * Goal selection screen
    * Would appear the first time after logging in at the beginning of
      each week
    * Auto-suggest one (for now, just whatever is at the top)
  * Goal management screen 
    * Add/edit/remove goals
* ## Other ideas
  * Record difficulty of facets
    * On a 1 (low) to 5 (high) scale
  * Warn people when they try to do difficult facets near the beginning
  * Authentication would have to be Facebook logins
    * Facebook Notifications would be used (maximum 180 characters)
    * [Facebook perimssions reference](https://developers.facebook.com/docs/facebook-login/permissions)
      * `public_profile` has all I should need
      * `user_friends` down the road might be nice for communal support
      * `email` For down the road sending reports (weekly, monthly)
* ## Encouragement
  * This is the key feature
  * The Facebook notifications should help
* ## Total time spent
  * The maximum number of goals to do is 52
    * For now. Eventually allow variable "campaigns"
  * total_time = login_time + week_number * review_time
    * Assuming login_time = 10 seconds, 52 weeks, and 3 seconds to review,
      the expected time will be under 3 minutes per day required to log
* ## Database
  * Tables
    * `facet` - A list of things to improve
      * `difficulty` (`int default 0`)
    * `campaign` - Series of facets to improve
      * Start date (`datetime`)
      * Time to send reminder
      * First day of week (if you'd like your new goals to start a day
        other than Sunday)
    * `user` - Self explanatory
      * Preferred time(s) to remind user to create a daily log
      * Cached first & last name
      * Join date
    * `log` - Main log table
      * Date & time
      * `user_id`
    * `log_facet` - Associates log entries to facets
      * Completed successfully?
        * In the future, if the facet is a weekly thing, and it's already
          been completed, auto-complete the facet by adding this
          entry automatically
      * `facet_id`
      * `log_id`