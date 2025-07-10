SET SESSION li_authorization_user = 'lmssalesops';  

SELECT 
  SB.crm_geo_region,
  SB.crm_market,
  SB.crm_rep_name AS Book_name,
  user.book_user_name AS Rep_name,
  GSO.SD_Group,
  SB.crm_rep_region,
  AC.ultimate_parent_sfdc_accountid,
  AC.ultimate_parent_sfdc_name,
  SB.crm_account_id,
  SB.crm_account_name,
  --SB.li_business_vertical,
  SB.deal_source,
  SB.advertiser_id,
  SB.crm_opportunity_id
  --SB.campaign_id,
 --SB.campaign_type_name,
 --GSO.lms_vertical,
 --GSO.crm_sub_vertical,
 --SB.delivery_currency
  --,SB.company_id 
  
,SUM(CASE WHEN event_date BETWEEN '2022-07-01' AND '2022-09-30' THEN recognized_amount_usd_current_rate ELSE 0 END) AS Q1FY23
,SUM(CASE WHEN event_date BETWEEN '2022-10-01' AND '2022-12-31' THEN recognized_amount_usd_current_rate ELSE 0 END) AS Q2FY23
,SUM(CASE WHEN event_date BETWEEN '2023-01-01' AND '2023-03-31' THEN recognized_amount_usd_current_rate ELSE 0 END) AS Q3FY23
,SUM(CASE WHEN event_date BETWEEN '2023-04-01' AND '2023-06-30' THEN recognized_amount_usd_current_rate ELSE 0 END) AS Q4FY23

,SUM(case when event_date between '2023-07-01' and '2023-09-30' THEN recognized_amount_usd_current_rate else 0 end) as Q1FY24
,SUM(case when event_date between '2023-10-01' and '2023-12-31' then recognized_amount_usd_current_rate else 0 end) as Q2FY24
,SUM(case when event_date between '2024-01-01' and '2024-03-31' then recognized_amount_usd_current_rate else 0 end) as Q3FY24
,SUM(case when event_date between '2024-04-01' and '2024-06-30' then recognized_amount_usd_current_rate else 0 end) as Q4FY24

,SUM(case when event_date between '2024-07-01' and '2024-09-30' then recognized_amount_usd_current_rate else 0 end) as Q1FY25
,sum(case when event_date between '2024-10-01' and '2024-12-31' then recognized_amount_usd_current_rate else 0 end) as Q2FY25
,sum(case when event_date between '2025-01-01' and '2025-03-31' then recognized_amount_usd_current_rate else 0 end) as Q3FY25
,sum(case when event_date between '2025-04-01' and '2025-06-30' then recognized_amount_usd_current_rate else 0 end) as Q4FY25

FROM foundation_lms_mp.agg_f_sas_campaign_summary SB

LEFT JOIN enterprise_crm_mp.dim_crm_account AC
ON crm_account_id=AC.id

LEFT JOIN (SELECT * FROM u_lmssalesops.dim_book_user WHERE book_user_role = 'MS_Account Executive') user
ON SB.crm_rep_id=user.book_owner_id

LEFT JOIN u_metrics.dim_lms_gso_info GSO
  ON SB.campaign_id=GSO.campaign_id

WHERE 1=1
--AND AC.ultimate_parent_sfdc_accountid IN ('0016000000S1D2LAAV')
--AND SB.crm_account_id IN ('0010d00001LABJwAAP')
--AND SB.advertiser_id IN (508378426,513746020,507034235,511622318)
--AND SB.crm_opportunity_id IN ('0060d00001sRq0PAAS')

--AND SB.crm_geo_region IN ('APAC','CHINA')
--AND SB.crm_market IN ('SG')
--AND SB.crm_rep_region LIKE 'LMS-AP%ESG%'

GROUP BY 1,2,3,4,5,5,6,7,8,9,10,11,12,13
ORDER BY 1,2,3,4,5,6,8,9,10,11,12,13
;
