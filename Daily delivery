SET SESSION li_authorization_user = 'lmssalesops'; 

SELECT * FROM (

            SELECT
            
        A.ultimate_parent_sfdc_name,
		A.crm_account_name,
		A.crm_rep_name AS Book_name,
		A.CRM_REP_REGION,
		A.EVENT_DATE AS "Date"
--                    ,         CAST(A.ONLINE_DELIVERY AS INT) AS "Delivery - Daily Online"
--                    ,         CAST(A.FIELD_DELIVERY AS INT) AS "Delivery - Daily Field IO"
                      ,         CAST(A.TOTAL_DELIVERY AS INT) AS "Daily Delivery"
                      ,         CAST(SUM(TOTAL_DELIVERY) OVER (ORDER BY EVENT_DATE DESC ROWS BETWEEN 0 FOLLOWING AND 6 FOLLOWING) AS INT) AS "Delivery - Running L7D"
      ,         CAST(SUM(TOTAL_DELIVERY) OVER (ORDER BY EVENT_DATE ASC ROWS UNBOUNDED PRECEDING) AS INT) AS "Delivery - Cumulative QTD"
                      
            FROM (
            
                SELECT
                AC.ultimate_parent_sfdc_name,
				SB.crm_account_name,
				SB.crm_rep_name,
				SB.CRM_REP_REGION,
				EVENT_DATE
                             ,          ROUND(SUM(CASE WHEN SB.DEAL_SOURCE = 'ONLINE' THEN RECOGNIZED_AMOUNT_USD_PLANNED_RATE ELSE 0 END),0) AS ONLINE_DELIVERY
                             ,          ROUND(SUM(CASE WHEN SB.DEAL_SOURCE = 'IO' THEN RECOGNIZED_AMOUNT_USD_PLANNED_RATE ELSE 0 END), 0) AS FIELD_DELIVERY
                             ,          ROUND(SUM(RECOGNIZED_AMOUNT_USD_PLANNED_RATE), 0) AS TOTAL_DELIVERY
                            
                FROM FOUNDATION_LMS_MP.AGG_F_SAS_CAMPAIGN_SUMMARY SB
                
				LEFT JOIN enterprise_crm_mp.dim_crm_account AC
				ON crm_account_id=AC.id
				
				WHERE DATE(EVENT_DATE) >= DATE('2025-01-01')
                    AND SB.CRM_REP_REGION LIKE 'LMS-AP%ESG%'
					--AND SB.crm_rep_name IN ('Book ESG SEA 2 Book 6')
				--AND AC.ultimate_parent_sfdc_accountid IN ('0016000000dD1lyAAC')
				--AND SB.advertiser_id IN (512349995)
                
                GROUP BY 1,2,3,4,5
                
        ) A

WHERE A.EVENT_DATE >= '2022-07-01'
    ) A;
