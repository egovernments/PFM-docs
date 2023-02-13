# Migration Checklist

This migration will require the following tasks to be performed:

## iFIX Core

1. Copy data to ElasticSearch
   * [ ] Fiscal Events
2. Copy data to PostgreSQL
   * [ ] iFIX Master Data Service
     * [ ] Government
     * [ ] Chart of Accounts
   * [ ] Fiscal Events

## iFIX Adapter

Apart from iFIX-Core, the other services relying on MongoDB were also migrated to PostgreSQL. So they will also need to be migrated.

1. Department Entity Service
   * [ ] Department Hierarchy Level
   * [ ] Department Entity
2. Adapter Master Data Service
   * [ ] Expenditure
   * [ ] Department
   * [ ] Project
