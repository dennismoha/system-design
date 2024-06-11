# Performance metrics
    https://youtu.be/HrfgslRY7Ak?list=PLTCrU9sGyburBw9wNOHebv9SjlE4Elv5a

When evaluating the performance of a system, several key metrics provide insight into how well the system is working. These metrics help identify bottlenecks, measure efficiency, and ensure the system meets performance requirements. Four fundamental concepts related to performance metrics are throughput, bandwidth, latency, and response time. Here's an overview of each concept:

### 1. Throughput

**Definition**: Throughput is the rate at which a system processes data or transactions over a specified period. It measures the amount of work performed by the system in a given time frame.

- **Measurement**: Typically expressed in transactions per second (TPS), requests per second (RPS), or data processed per second (e.g., bytes/second).
- **Significance**: High throughput indicates that a system can handle a large volume of work efficiently. It is crucial for systems requiring high processing capabilities, such as web servers, databases, and data processing pipelines.
- **Factors Influencing Throughput**: System resources (CPU, memory, I/O), concurrency level, system architecture, and workload characteristics.

### 2. Bandwidth

**Definition**: Bandwidth refers to the maximum rate at which data can be transferred across a network or a communication channel. It represents the capacity of the system to transmit data.

- **Measurement**: Expressed in bits per second (bps), kilobits per second (Kbps), megabits per second (Mbps), or gigabits per second (Gbps).
- **Significance**: High bandwidth indicates a higher capacity for data transfer, which is essential for applications requiring large data transfers, such as video streaming, file transfers, and high-performance computing.
- **Factors Influencing Bandwidth**: Network infrastructure, communication protocols, and physical medium (e.g., fiber optic cables, wireless).

### 3. Latency

**Definition**: Latency is the time delay between the initiation of a request and the completion of the corresponding response. It measures how quickly a system can respond to a request.

- **Measurement**: Expressed in milliseconds (ms) or microseconds (µs).
- **Significance**: Low latency is critical for real-time applications, such as online gaming, financial trading, and interactive web applications, where delays can significantly impact user experience or system performance.
- **Factors Influencing Latency**: Network delays, processing time, queuing delays, and system load.

### 4. Response Time

**Definition**: Response time is the total time taken for a system to respond to a request. It includes latency and the time required to process and return the result.

- **Measurement**: Expressed in milliseconds (ms) or seconds (s).
- **Significance**: Low response time enhances user experience by providing quicker feedback to user actions. It is a critical metric for web applications, APIs, and any interactive system.
- **Factors Influencing Response Time**: Server processing speed, system load, network latency, and efficiency of the application code.

### Interrelationship of Metrics

- **Throughput vs. Bandwidth**: Throughput is often constrained by bandwidth. If the bandwidth is limited, it can cap the maximum throughput achievable by the system.
- **Latency vs. Response Time**: Latency is a component of response time. Reducing latency directly reduces response time, improving the perceived speed of the system.
- **Throughput vs. Latency**: In some systems, increasing throughput can lead to higher latency due to congestion and resource contention. Balancing these metrics is key to optimizing performance.
- **Bandwidth vs. Latency**: High bandwidth can help reduce latency in data transfer by allowing more data to be transmitted simultaneously, but it doesn't eliminate the inherent propagation delay.

### Summary

Understanding and measuring these performance metrics—throughput, bandwidth, latency, and response time—are essential for evaluating and optimizing system performance. Each metric provides unique insights, and their interrelationships highlight the need for a balanced approach to performance tuning and resource allocation.

# Javascript Apps to Measure Throughput

When it comes to measuring throughput in JavaScript, particularly for web applications, there are several libraries and tools that can help you generate load, measure performance, and analyze throughput. Here are some JavaScript tools and libraries suitable for measuring throughput:

### 1. Artillery

**Description**: Artillery is a modern, powerful, and easy-to-use load testing toolkit. It’s designed for testing backend APIs and microservices, but it can also be used to test web applications.

**Features**:
- Supports HTTP, WebSocket, and other protocols.
- Provides detailed performance reports.
- Allows for writing test scenarios in JSON or YAML.

**Installation**:
```sh
npm install -g artillery
```

**Usage**:
Create a test script in YAML:
```yaml
config:
  target: 'http://your-api.com'
  phases:
    - duration: 60
      arrivalRate: 10
scenarios:
  - flow:
      - get:
          url: "/endpoint"
```

Run the test:
```sh
artillery run your-test-script.yml
```

### 2. k6

**Description**: k6 is a modern load testing tool that provides a developer-centric CLI and JavaScript scripting API.

**Features**:
- Scripting in JavaScript with ES6 features.
- Detailed and actionable performance insights.
- Integrates with CI/CD pipelines.

**Installation**:
```sh
brew install k6
```

**Usage**:
Create a test script in JavaScript:
```javascript
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
  stages: [
    { duration: '30s', target: 20 },
    { duration: '1m30s', target: 10 },
    { duration: '20s', target: 0 },
  ],
};

export default function () {
  let res = http.get('http://your-api.com/endpoint');
  check(res, { 'status was 200': (r) => r.status == 200 });
  sleep(1);
}
```

Run the test:
```sh
k6 run your-test-script.js
```

### 3. autocannon

**Description**: autocannon is a fast HTTP/1.1 benchmarking tool written in Node.js.

**Features**:
- Designed to be fast and lightweight.
- Simple CLI interface.
- Can be used programmatically within Node.js applications.

**Installation**:
```sh
npm install -g autocannon
```

**Usage**:
Run a basic test:
```sh
autocannon -c 10 -d 10 -p 10 http://your-api.com/endpoint
```

Use programmatically:
```javascript
const autocannon = require('autocannon');

autocannon({
  url: 'http://your-api.com/endpoint',
  connections: 10,
  duration: 10
}, console.log);
```

### 4. Loadtest

**Description**: Loadtest is a simple command-line tool for load testing and benchmarking web services.

**Features**:
- Easy to use with minimal configuration.
- Supports custom headers and POST data.
- Can be used programmatically.

**Installation**:
```sh
npm install -g loadtest
```

**Usage**:
Run a basic test:
```sh
loadtest -n 1000 -c 10 http://your-api.com/endpoint
```

Use programmatically:
```javascript
const loadtest = require('loadtest');

const options = {
  url: 'http://your-api.com/endpoint',
  maxRequests: 1000,
  concurrency: 10,
};

loadtest.loadTest(options, (error, result) => {
  if (error) {
    return console.error('Got an error: %s', error);
  }
  console.log('Tests run successfully:', result);
});
```

### Summary

These tools and libraries provide a range of capabilities for measuring throughput in JavaScript applications. **Artillery** and **k6** are robust choices for detailed load testing and performance analysis, while **autocannon** and **loadtest** offer simpler, yet powerful options for quick benchmarking and stress testing. Depending on your specific needs and environment, you can choose the tool that best fits your requirements for measuring throughput and optimizing performance.

# Performance Metrics of an Application

Evaluating the performance of an application involves several key metrics that provide insight into how well the application is functioning. Here are four important performance metrics and how to measure them effectively in the context of APIs:

### 1. API Response Time

**Definition**: API response time is the time taken for an API to process a request and return a response. It includes the time spent in the network, server processing, and any intermediate steps.

**How to Measure**:
- **Tools**: Use tools like Postman, Apache JMeter, or k6 to measure response times.
- **Metrics**: Track the average response time, 95th percentile response time, and maximum response time.

**Example**:
```javascript
import http from 'k6/http';
import { check } from 'k6';

export default function () {
  let res = http.get('http://your-api.com/endpoint');
  check(res, { 'response time was <= 200ms': (r) => r.timings.duration <= 200 });
}
```

**Monitoring**:
- Use application performance monitoring (APM) tools like New Relic, Datadog, or Grafana to continuously monitor response times in real-time.

### 2. Throughput of APIs

**Definition**: Throughput is the number of API requests processed per second or minute. It measures the capacity of the API to handle concurrent requests.

**How to Measure**:
- **Tools**: Use load testing tools such as Apache JMeter, k6, or Artillery.
- **Metrics**: Track the number of requests per second (RPS) or transactions per second (TPS).

**Example**:
```yaml
config:
  target: 'http://your-api.com'
  phases:
    - duration: 60
      arrivalRate: 10
scenarios:
  - flow:
      - get:
          url: "/endpoint"
```

**Monitoring**:
- Integrate with monitoring tools to visualize throughput metrics. Use Grafana with Prometheus or similar stacks to create dashboards showing throughput over time.

### 3. Error Occurrences

**Definition**: Error occurrences measure the number of failed API requests. This includes client errors (4xx status codes) and server errors (5xx status codes).

**How to Measure**:
- **Tools**: Use logging and monitoring tools like ELK Stack (Elasticsearch, Logstash, Kibana), Sentry, or New Relic.
- **Metrics**: Track the number of errors per minute or the error rate (percentage of failed requests).

**Example**:
```javascript
import http from 'k6/http';
import { check } from 'k6';

export default function () {
  let res = http.get('http://your-api.com/endpoint');
  check(res, { 'status is 200': (r) => r.status === 200 });
}
```

**Monitoring**:
- Set up alerts in your monitoring tools to notify you of error spikes. Use thresholds and anomaly detection to identify issues quickly.

### 4. Bugs / Defects in the Code

**Definition**: Bugs or defects in the code refer to issues in the application logic that cause incorrect behavior, performance degradation, or security vulnerabilities.

**How to Measure**:
- **Tools**: Use static code analysis tools like SonarQube, ESLint, and security scanners like OWASP ZAP.
- **Metrics**: Track the number of defects identified per release, the severity of the defects, and the time taken to resolve them.

**Example**:
- **Static Analysis**: Integrate ESLint into your CI/CD pipeline to catch coding issues early.
- **Security Scanning**: Run OWASP ZAP scans as part of your CI/CD pipeline to identify security vulnerabilities.

**Monitoring**:
- Maintain a bug tracker (e.g., Jira, GitHub Issues) to log and track the progress of bug fixes.
- Use dashboards to visualize defect trends over time and identify areas needing improvement.

### Summary

To effectively evaluate and improve the performance of your application, it is essential to monitor API response time, throughput, error occurrences, and bugs/defects. Utilizing appropriate tools and integrating them into your development and monitoring workflows ensures that you can identify and address performance issues promptly. This holistic approach helps maintain high performance and reliability of your application.

# Perfomance metrics of a database system.

Measuring the performance of a database system involves more than just tracking query execution times. Comprehensive performance metrics provide a deeper understanding of the system's efficiency, scalability, and reliability. Here are some essential performance metrics for evaluating a database system:

### 1. Query Execution Time

**Definition**: The time taken for a database to execute a query from the moment it is received to the moment the result is returned.

**How to Measure**:
- **Tools**: Use database profiling and logging tools like `EXPLAIN` in SQL, APM tools like New Relic, Datadog, or database-specific tools like MySQL’s `slow query log`.
- **Metrics**: Average execution time, 95th percentile execution time, maximum execution time.

**Example**:
```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE id = 1;
```

**Monitoring**:
- Continuously monitor query performance using APM tools or built-in database performance dashboards.

### 2. Throughput

**Definition**: The number of transactions processed by the database per unit of time, usually measured in transactions per second (TPS) or queries per second (QPS).

**How to Measure**:
- **Tools**: Use performance benchmarking tools like Sysbench, HammerDB, or database built-in metrics.
- **Metrics**: Transactions per second (TPS), queries per second (QPS).

**Example**:
```bash
sysbench --test=oltp --mysql-table-engine=innodb --oltp-table-size=1000000 --mysql-db=test --mysql-user=root --mysql-password=yourpassword run
```

**Monitoring**:
- Regularly review throughput metrics using database monitoring tools and set up alerts for significant drops.

### 3. Concurrency and Locking

**Definition**: Measures how well the database handles concurrent operations and the impact of locking on performance.

**How to Measure**:
- **Tools**: Use database monitoring tools that track lock waits and deadlocks, such as pg_stat_activity for PostgreSQL or InnoDB Monitor for MySQL.
- **Metrics**: Number of active connections, lock wait time, number of deadlocks.

**Example**:
```sql
SHOW ENGINE INNODB STATUS;  -- For MySQL
SELECT * FROM pg_stat_activity;  -- For PostgreSQL
```

**Monitoring**:
- Monitor the number of active and waiting connections, lock waits, and deadlocks using performance dashboards.

### 4. Resource Utilization

**Definition**: Measures the usage of system resources (CPU, memory, disk I/O) by the database system.

**How to Measure**:
- **Tools**: Use system monitoring tools like top, iostat, vmstat, or database-specific tools like MySQL Performance Schema, PostgreSQL pg_stat_statements.
- **Metrics**: CPU utilization, memory usage, disk I/O, buffer cache hit ratio.

**Example**:
```sql
SELECT * FROM performance_schema.host_summary;  -- For MySQL
SELECT * FROM pg_stat_statements;  -- For PostgreSQL
```

**Monitoring**:
- Regularly monitor resource utilization metrics using system and database-specific monitoring tools to ensure optimal resource usage.

### 5. Index Performance

**Definition**: Measures the effectiveness of indexes in speeding up query performance.

**How to Measure**:
- **Tools**: Use database tools to analyze index usage, like `EXPLAIN` in SQL, or specific tools like pt-index-usage for MySQL.
- **Metrics**: Index hit ratio, number of index scans, index maintenance overhead.

**Example**:
```sql
EXPLAIN SELECT * FROM users WHERE username = 'john_doe';  -- Check index usage
```

**Monitoring**:
- Continuously monitor index performance and usage statistics to identify unused or inefficient indexes.

### 6. Cache Hit Ratio

**Definition**: The ratio of database read requests satisfied by the cache compared to the total read requests.

**How to Measure**:
- **Tools**: Use database metrics tools like MySQL Performance Schema or PostgreSQL pg_stat_database.
- **Metrics**: Buffer cache hit ratio, page cache hit ratio.

**Example**:
```sql
SHOW STATUS LIKE 'Qcache%';  -- For MySQL
SELECT * FROM pg_stat_database;  -- For PostgreSQL
```

**Monitoring**:
- Regularly monitor cache hit ratios to ensure that the database is efficiently using its cache.

### 7. Error Rate

**Definition**: The frequency of errors occurring during database operations, including query errors, connection issues, and transaction failures.

**How to Measure**:
- **Tools**: Use database logs, error tracking tools, and APM tools to track error occurrences.
- **Metrics**: Number of errors per minute, error rate as a percentage of total queries.

**Example**:
```sql
SHOW GLOBAL STATUS LIKE 'Aborted%';  -- For MySQL
SELECT * FROM pg_stat_activity WHERE state = 'idle in transaction';  -- For PostgreSQL
```

**Monitoring**:
- Set up alerts for error spikes and regularly review error logs to identify and address recurring issues.

### Summary

By measuring these key performance metrics—query execution time, throughput, concurrency and locking, resource utilization, index performance, cache hit ratio, and error rate—you can gain a comprehensive understanding of your database system’s performance. Using appropriate tools and continuous monitoring helps in identifying bottlenecks, optimizing performance, and ensuring the reliability and efficiency of your database.

# Query optimization 

### 8. Query Optimization

**Definition**: The efficiency of how queries are written and executed can significantly impact database performance. Poorly written or unoptimized queries can lead to slower performance, increased resource consumption, and longer execution times.

**How to Measure**:
- **Tools**: Use query analysis and profiling tools like `EXPLAIN` in SQL, query optimizers, and performance monitoring tools.
- **Metrics**: Query execution plans, number of joins, use of indexes, execution time, and resource consumption (CPU, memory, I/O).

**Example**:
```sql
EXPLAIN ANALYZE SELECT * FROM users WHERE id = 1;
```

**Monitoring**:
- Regularly review and optimize query execution plans using the `EXPLAIN` statement and query profiling tools.
- Use APM tools to identify slow queries and understand their impact on overall performance.

### How Unoptimized Queries Affect Performance

1. **Excessive Full Table Scans**:
   - Queries that do not use indexes may result in full table scans, which are expensive and slow.
   - Example: 
     ```sql
     SELECT * FROM users WHERE LOWER(username) = 'john_doe';  -- This might not use an index on `username`
     ```

2. **Inefficient Joins**:
   - Complex joins and subqueries can significantly slow down query performance, especially if not indexed correctly.
   - Example:
     ```sql
     SELECT u.*, o.* FROM users u JOIN orders o ON u.id = o.user_id WHERE u.status = 'active';
     ```

3. **Poor Use of Indexes**:
   - Not using indexes effectively can lead to increased I/O and slower query times. Indexes should be used on columns frequently involved in WHERE, JOIN, and ORDER BY clauses.
   - Example:
     ```sql
     SELECT * FROM orders WHERE order_date > '2024-01-01';  -- Ensure `order_date` is indexed
     ```

4. **Redundant Data Retrieval**:
   - Fetching more data than necessary, such as using `SELECT *`, can lead to increased memory usage and slower performance.
   - Example:
     ```sql
     SELECT * FROM large_table;  -- Only select necessary columns
     ```

5. **Lack of Query Caching**:
   - Not leveraging query caching mechanisms can lead to repeated execution of the same queries, reducing performance.
   - Example:
     ```sql
     SELECT COUNT(*) FROM users WHERE active = true;  -- Cache results if frequently used
     ```

### Optimization Techniques

1. **Indexing**:
   - Create indexes on columns that are frequently used in WHERE clauses, JOIN conditions, and ORDER BY clauses.
   - Example:
     ```sql
     CREATE INDEX idx_username ON users(username);
     ```

2. **Query Refactoring**:
   - Simplify complex queries and break them into smaller, more manageable parts if necessary.
   - Example:
     ```sql
     -- Instead of a complex join
     SELECT u.*, o.* FROM users u JOIN orders o ON u.id = o.user_id WHERE u.status = 'active';

     -- Refactor to optimize
     CREATE TEMPORARY TABLE active_users AS SELECT id FROM users WHERE status = 'active';
     SELECT u.*, o.* FROM active_users au JOIN orders o ON au.id = o.user_id;
     ```

3. **Avoiding SELECT ***:
   - Select only the necessary columns to reduce data retrieval overhead.
   - Example:
     ```sql
     SELECT id, username, email FROM users WHERE status = 'active';
     ```

4. **Using Query Caching**:
   - Implement query caching mechanisms to store the results of frequently executed queries.
   - Example:
     ```sql
     SET query_cache_type = ON;
     ```

5. **Regular Maintenance**:
   - Perform regular database maintenance tasks like updating statistics, defragmenting indexes, and analyzing tables.
   - Example:
     ```sql
     ANALYZE TABLE users;
     ```

### Summary

Optimizing queries is a crucial aspect of database performance management. By writing efficient queries and continuously monitoring their performance, you can ensure that your database runs smoothly and efficiently. Leveraging the right tools and techniques for query analysis, indexing, and refactoring will help minimize execution times and resource consumption, leading to a more performant and reliable database system.

# Performanc metrics of Cache

When evaluating the performance of a caching system, several key metrics provide valuable insights into its efficiency and effectiveness. Here are some essential performance metrics for caching systems:

### 1. Latency of Writing to Cache

**Definition**: The time it takes to write data to the cache. Lower latency indicates a faster and more efficient caching system.

**How to Measure**:
- **Tools**: Use performance monitoring tools that support cache metrics such as Redis' built-in monitoring commands (`INFO`), Memcached statistics, or APM tools like New Relic and Datadog.
- **Metrics**: Average write latency, 95th percentile write latency, maximum write latency.

**Example (Redis)**:
```shell
redis-cli --latency
```

**Monitoring**:
- Continuously track write latency using monitoring tools and set up alerts for spikes in latency to promptly address any issues.

### 2. Number of Cache Evictions and Invalidations

**Definition**: The number of times items are evicted from the cache due to capacity limits or invalidated due to data changes. High eviction rates can indicate insufficient cache size or improper cache configuration.

**How to Measure**:
- **Tools**: Use cache-specific monitoring tools and commands, such as Redis' `INFO` command or Memcached's `stats` command.
- **Metrics**: Number of evictions per second, total evictions, number of invalidations per second, total invalidations.

**Example (Redis)**:
```shell
redis-cli INFO stats | grep evicted_keys
```

**Monitoring**:
- Regularly monitor eviction and invalidation rates to ensure the cache is appropriately sized and configured. High eviction rates may indicate a need for increased cache size or changes to eviction policies.

### 3. Memory Usage of Cache Instance

**Definition**: The amount of memory used by the cache instance. Effective memory management ensures the cache operates within its capacity without causing performance degradation.

**How to Measure**:
- **Tools**: Use cache-specific tools and commands to monitor memory usage, such as Redis' `INFO` command or Memcached's `stats` command.
- **Metrics**: Current memory usage, peak memory usage, percentage of memory used.

**Example (Redis)**:
```shell
redis-cli INFO memory | grep used_memory
```

**Monitoring**:
- Continuously monitor memory usage to ensure the cache instance operates within its allocated memory. Set up alerts for high memory usage to prevent out-of-memory issues.

### Summary of Cache Performance Metrics

1. **Latency of Writing to Cache**:
   - **Definition**: Time taken to write data to the cache.
   - **How to Measure**: Use tools like Redis' `INFO`, Memcached stats, and APM tools.
   - **Metrics**: Average, 95th percentile, and maximum write latency.

2. **Number of Cache Evictions and Invalidations**:
   - **Definition**: Frequency of item evictions due to capacity limits or invalidations due to data changes.
   - **How to Measure**: Use cache-specific monitoring tools and commands.
   - **Metrics**: Evictions per second, total evictions, invalidations per second, total invalidations.

3. **Memory Usage of Cache Instance**:
   - **Definition**: Amount of memory used by the cache.
   - **How to Measure**: Use cache-specific tools like Redis' `INFO` or Memcached's `stats`.
   - **Metrics**: Current memory usage, peak memory usage, percentage of memory used.

### Example Commands and Monitoring Setup

For Redis:

- **Latency of Writing to Cache**:
  ```shell
  redis-cli --latency
  ```

- **Number of Cache Evictions and Invalidations**:
  ```shell
  redis-cli INFO stats | grep evicted_keys
  ```

- **Memory Usage of Cache Instance**:
  ```shell
  redis-cli INFO memory | grep used_memory
  ```

For Memcached:

- **Latency of Writing to Cache**:
  ```shell
  echo "stats" | nc localhost 11211 | grep evictions
  ```

- **Number of Cache Evictions and Invalidations**:
  ```shell
  echo "stats" | nc localhost 11211 | grep evictions
  ```

- **Memory Usage of Cache Instance**:
  ```shell
  echo "stats" | nc localhost 11211 | grep bytes
  ```

### Monitoring and Alerting

Use monitoring tools like New Relic, Datadog, or built-in monitoring dashboards to continuously track these metrics. Set up alerts for thresholds, such as high latency, high eviction rates, or high memory usage, to proactively manage and optimize cache performance.

By monitoring and optimizing these key performance metrics, you can ensure your caching system operates efficiently, providing quick access to frequently used data and improving overall application performance.