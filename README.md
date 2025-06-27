**DuckLake Demo — PostgreSQL + MinIO Setup**
This project uses Docker Compose to run:

 **PostgreSQL** — to store DuckLake metadata (schemas, snapshots, manifests)

 **MinIO** (S3 compatible) — to store your Parquet data files in object storage
 
 **How to Run**
1️⃣ **Start services**
  docker-compose up -d
2️⃣ **Verify containers are running or not** 
  docker ps

3️⃣ **Access PostgreSQL**
  Host: localhost
  Port: 5432
  User: ducklake
  Password: ducklake
You can connect using:
  psql -h localhost -U ducklake -d ducklake
  
4️⃣ **Access MinIO**
  URL: http://localhost:9001
  User: admin
  Password: password
  
➡️ **Use DuckDB locally to connect:**

  **PostgreSQL** as the DuckLake catalog backend
  **MinIO** as the data storage for Parquet files
Example DuckDB attach command:
  ATTACH 'ducklake:postgres:host=localhost dbname=ducklake user=ducklake password=ducklake port=5432'
    AS my_ducklake (data_path 's3://warehouse/');
    
**Note:** Make sure you have:
  DuckLake extension installed in DuckDB
  MinIO credentials set properly if needed 

**Stop & Clean Up**
To stop:
  docker-compose down
**To remove volumes too:**
  docker-compose down -v

 
