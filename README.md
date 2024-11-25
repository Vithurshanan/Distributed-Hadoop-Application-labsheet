Here is a **README.md** file for your project based on the steps provided:

```markdown
# HDFS WordCount using Docker and Hadoop

This project demonstrates how to use Docker to set up an HDFS environment and execute a MapReduce WordCount program. Below are the steps to get started.

## Prerequisites

- Docker and Docker Compose installed on your system
- A file named `sample.txt` to use as input for the WordCount program

## Steps to Run the Project

1. **Start the Docker containers**  
   Launch the Hadoop cluster using Docker Compose:
   ```bash
   docker-compose up -d
   ```

2. **Copy the input file to the namenode**  
   Use the `docker cp` command to copy `sample.txt` to the namenode container:
   ```bash
   docker cp "/path/to/your/sample.txt" namenode:/sample.txt
   ```

3. **Verify the file in the namenode**  
   List the files in the root directory of the namenode container to confirm the file was copied:
   ```bash
   docker exec -it namenode ls /
   ```

4. **Create an HDFS input directory**  
   Create an input directory in HDFS:
   ```bash
   docker exec -it namenode hdfs dfs -mkdir -p /input
   ```

5. **Upload the file to HDFS**  
   Put the `sample.txt` file into the HDFS input directory:
   ```bash
   docker exec -it namenode hdfs dfs -put /sample.txt /input
   ```

6. **Verify the file in HDFS**  
   List the contents of the HDFS input directory to confirm the file was uploaded:
   ```bash
   docker exec -it namenode hdfs dfs -ls /input
   ```

7. **Run the WordCount MapReduce job**  
   Execute the Hadoop WordCount example jar to process the input file:
   ```bash
   docker exec -it namenode hadoop jar /opt/hadoop-3.2.1/share/hadoop/mapreduce/hadoop-mapreduce-examples-3.2.1.jar wordcount /input /output
   ```

8. **Verify the WordCount output**  
   List the files in the HDFS output directory:
   ```bash
   docker exec -it namenode hdfs dfs -ls /output
   ```

9. **Display the WordCount results**  
   View the output of the WordCount program:
   ```bash
   docker exec -it namenode hdfs dfs -cat /output/part-r-00000
   ```

10. **Stop the Docker containers**  
    Shut down the Hadoop cluster:
    ```bash
    docker-compose down
    ```

## Notes

- Replace the path to `sample.txt` with the actual path where your input file is located.
- Ensure the `docker-compose.yml` file is properly set up for your Hadoop environment.
- The `part-r-00000` file contains the WordCount output, which lists each word and its frequency.

## Files in the Project

- `sample.txt`: Input file for the WordCount program
- `docker-compose.yml`: Configuration file for setting up the Hadoop cluster
- This `README.md` file

## Troubleshooting

1. **Container Not Found**: If the `namenode` container is not running, start it using:
   ```bash
   docker-compose up -d
   ```

2. **File Not Found in HDFS**: Double-check the path when copying or uploading files to ensure accuracy.

3. **Docker Command Errors**: Refer to the Docker documentation for more details on `docker cp`, `docker exec`, and `docker-compose` commands.

---

Enjoy experimenting with Hadoop and Docker!
```
