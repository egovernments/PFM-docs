# Migration to DIGIT Architecture

Migration to DIGIT architecture primarily involves the following changes to iFIX-Core:

1. Transactional DB is switched from MongoDB to PostgreSQL
2. Analytics DB is switched from Druid to ElasticSearch
   1. Correspondingly, the dashboard is switched from Metabase to the DSS dashboard
