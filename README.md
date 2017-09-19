# Mode_Analytics

Queries Used:

SELECT DATE_TRUNC('week', e.occurred_at),
       COUNT(DISTINCT e.user_id) AS weekly_active_users
  FROM tutorial.yammer_events e
 WHERE e.event_type = 'engagement'
   AND e.event_name = 'login'
 GROUP BY 1
 ORDER BY 1
 
 SELECT DATE_TRUNC('week', e.occurred_at),
       COUNT(DISTINCT e.user_id) AS weekly_signups
  FROM tutorial.yammer_events e
 WHERE e.event_type = 'signup_flow'
   AND e.event_name = 'create_user'
 GROUP BY 1
 ORDER BY 1
 
 SELECT DATE_TRUNC('week', occurred_at),
       COUNT(CASE WHEN event_name = 'home_page' THEN user_id ELSE NULL END) AS weekly_homepage,
       COUNT(CASE WHEN event_name = 'view_inbox' THEN user_id ELSE NULL END) AS weekly_inbox,
       COUNT(CASE WHEN event_name = 'search_run' THEN user_id ELSE NULL END) AS weekly_search,
       COUNT(CASE WHEN event_name = 'send_message' THEN user_id ELSE NULL END) AS weekly_send,
       COUNT(CASE WHEN event_name = 'like_message' THEN user_id ELSE NULL END) AS weekly_like
  FROM tutorial.yammer_events
 WHERE event_type = 'engagement'
 GROUP BY 1
 ORDER BY 1
 
 SELECT DATE_TRUNC('week', e.occurred_at),
       e.location,
       COUNT(DISTINCT e.user_id) AS weekly_active_users
  FROM tutorial.yammer_events e
 WHERE e.event_type = 'engagement'
   AND e.event_name = 'login'
   AND e.location IN ('United States', 'Italy', 'Russia', 'Japan', 'Germany', 'Canada', 'Brazil', 'India', 'France')
 GROUP BY 1, 2
 ORDER BY 1, 2
 
 SELECT DATE_TRUNC('week', e.occurred_at),
       e.location,
       COUNT(DISTINCT e.user_id) AS weekly_active_users
  FROM tutorial.yammer_events e
 WHERE e.event_type = 'engagement'
   AND e.event_name = 'login'
   AND e.location IN ('Italy', 'Russia', 'Japan', 'Germany', 'Canada', 'Brazil', 'India', 'France')
 GROUP BY 1, 2
 ORDER BY 1, 2
 
 SELECT DATE_TRUNC('week', e.occurred_at),
       CASE WHEN e.device IN ('macbook pro','lenovo thinkpad','macbook air','dell inspiron notebook', 'asus chromebook','dell inspiron desktop','acer aspire notebook','hp pavilion desktop','acer aspire desktop','mac mini') THEN 'computer'
            WHEN e.device IN ('iphone 5','samsung galaxy s4','nexus 5','iphone 5s','iphone 4s','nokia lumia 635', 'htc one','samsung galaxy note','amazon fire phone') THEN 'phone'
            ELSE 'tablet' END AS device_type,
       COUNT(DISTINCT e.user_id) AS weekly_active_users
  FROM tutorial.yammer_events e
 WHERE e.event_type = 'engagement'
   AND e.event_name = 'login' 
 GROUP BY 1, 2
 ORDER BY 1, 2
 
 SELECT DATE_TRUNC('week', occurred_at) AS week,
       COUNT(CASE WHEN action = 'sent_weekly_digest' THEN user_id ELSE NULL END) AS weekly_emails,
       COUNT(CASE WHEN action = 'sent_reengagement_email' THEN user_id ELSE NULL END) AS reengagement_emails,
       COUNT(CASE WHEN action = 'email_open' THEN user_id ELSE NULL END) AS email_opens,
       COUNT(CASE WHEN action = 'email_clickthrough' THEN user_id ELSE NULL END) AS email_clickthroughs
  FROM tutorial.yammer_emails
 GROUP BY 1
 ORDER BY 1
