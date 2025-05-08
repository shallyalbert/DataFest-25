SELECT
    state,
    ROUND(AVG(CASE WHEN (year < 2020 OR (year = 2020 AND month < 3)) THEN unemployment_rate ELSE NULL END), 2) AS pre_pandemic_avg,
    ROUND(AVG(CASE WHEN (year > 2020 OR (year = 2020 AND month >= 3)) THEN unemployment_rate ELSE NULL END), 2) AS post_pandemic_avg,
    ROUND(
        AVG(CASE WHEN (year > 2020 OR (year = 2020 AND month >= 3)) THEN unemployment_rate ELSE NULL END) -
        AVG(CASE WHEN (year < 2020 OR (year = 2020 AND month < 3)) THEN unemployment_rate ELSE NULL END),
        2
    ) AS increase_in_rate
FROM unemployment_db
GROUP BY state
ORDER BY increase_in_rate DESC;

SELECT
    region,
    pandemic_period,
    ROUND(AVG(unemployment_rate), 2) AS avg_unemployment_rate
FROM (
    SELECT
        CASE
            WHEN state IN ("AK", "AZ", "CA", "CO", "HI", "ID", "MT", "NV", "NM", "OR", "UT", "WA", "WY") THEN 'West'
            WHEN state IN ("CT", "DE", "MA", "MD", "ME", "NH", "NJ", "NY", "PA", "RI", "VT", "DC") THEN 'East'
            WHEN state IN ("AL", "AR", "FL", "GA", "KY", "LA", "MS", "NC", "OK", "SC", "TN", "TX", "VA", "WV") THEN 'South'
            ELSE 'Other'  
        END AS region,
        unemployment_rate,
        CASE 
            WHEN year < 2020 OR (year = 2020 AND month < 3) THEN 'Pre-Pandemic'
            ELSE 'Post-Pandemic'
        END AS pandemic_period
    FROM unemployment_db
) AS region_data
GROUP BY region, pandemic_period
ORDER BY region, pandemic_period;
