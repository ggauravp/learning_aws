1. To show the data available in my local(mypc) database i have to import the database from my laptop to the ec2 instance database so that the data can be shown to the deployed website.
2. goto pgadmin and 
- pgAdmin → Backup → Plain → saved as main_job.sql
3. Copy main_job.sql from Windows/WSL to EC2 using `scp`
- `scp -i /path/to/test-keypair.pem /path/to/main_job.sql ubuntu@<EC2-IP>:~`
4. Create the database on EC2
- `sudo -u postgres psql`
- CREATE DATABASE job_recommendation;
- \q
5. Import SQL file into EC2 database
- `sudo -u postgres psql -d job_recommendation -f main_job.sql`
6. Verify tables and data
- `sudo -u postgres psql -d job_recommendation`
- `\dt`

7. Set up Django to use EC2 database<br>
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'job_recommendation',
        'USER': 'postgres',
        'PASSWORD': '<your_postgres_password>',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

- `python3 manage.py migrate`
