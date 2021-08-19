# CourseManagement_JPA_JSF
the main purpose of this project is to use JPA to access database


## Technologies

* Jdk1.8
* MySql 8.0.19
* Tomcat 9 
* Maven
* JPA
* JEE
* jsf
## Dependencies

1. Make sure you have [Java](http://www.java.com/) installed on your system, if not follow the vendor instructions for installing them on your operating system.
2. Make sure you have [MySql](https://dev.mysql.com/downloads/mysql/) installed on your system, if not follow the vendor instructions for installing them on your operating system.

## Highlights
* Database data definition scripts

* Instructions for server configuration in Eclipse EE and NetBeans



## Setup

### MySql
**EER Diagrame of the database**
* ![COURSE-MANGMENTSCHEMA_JPA](https://user-images.githubusercontent.com/62031222/130084268-ed2f4ad8-e877-48c4-92b8-678666c2b07f.png)
* run this script to create the schema 'course_management_jpa' and the tables

```
-- MySQL Script generated by MySQL Workbench
-- Model: New Model    Version: 1.0
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema course_management_jpa
-- -----------------------------------------------------
DROP SCHEMA IF EXISTS `course_management_jpa` ;

-- -----------------------------------------------------
-- Schema course_management_jpa
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `course_management_jpa` DEFAULT CHARACTER SET utf8 ;
USE `course_management_jpa` ;

-- -----------------------------------------------------
-- Table `course_management_jpa`.`Teacher`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `course_management_jpa`.`Teacher` ;

CREATE TABLE IF NOT EXISTS `course_management_jpa`.`Teacher` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `first_name` VARCHAR(45) NOT NULL,
  `last_name` VARCHAR(45) NULL,
  `designation` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `course_management_jpa`.`Course`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `course_management_jpa`.`Course` ;

CREATE TABLE IF NOT EXISTS `course_management_jpa`.`Course` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(45) NOT NULL,
  `credits` INT NOT NULL,
  `Teacher_id` INT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_Course_Teacher_idx` (`Teacher_id` ASC) VISIBLE,
  CONSTRAINT `fk_Course_Teacher`
    FOREIGN KEY (`Teacher_id`)
    REFERENCES `course_management_jpa`.`Teacher` (`id`)
    ON DELETE set null
    ON UPDATE cascade)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `course_management_jpa`.`Student`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `course_management_jpa`.`Student` ;

CREATE TABLE IF NOT EXISTS `course_management_jpa`.`Student` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `first_name` VARCHAR(45) NOT NULL,
  `last_name` VARCHAR(45) NULL,
  `enrolled_since`  date NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `course_management_jpa`.`Course_Student`
-- -----------------------------------------------------
DROP TABLE IF EXISTS `course_management_jpa`.`Course_Student` ;

CREATE TABLE IF NOT EXISTS `course_management_jpa`.`Course_Student` (
  `Course_id` INT NOT NULL,
  `Student_id` INT NOT NULL,
  PRIMARY KEY (`Course_id`, `Student_id`),
  INDEX `fk_Course_has_Student_Student1_idx` (`Student_id` ASC) VISIBLE,
  INDEX `fk_Course_has_Student_Course1_idx` (`Course_id` ASC) VISIBLE,
  CONSTRAINT `fk_Course_has_Student_Course1`
    FOREIGN KEY (`Course_id`)
    REFERENCES `course_management_jpa`.`Course` (`id`)
    ON DELETE cascade
    ON UPDATE cascade,
  CONSTRAINT `fk_Course_has_Student_Student1`
    FOREIGN KEY (`Student_id`)
    REFERENCES `course_management_jpa`.`Student` (`id`)
    ON DELETE cascade
    ON UPDATE cascade)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;


```

### Java EE Server - Apache Tomcat 9 
Download and extract [Tomcat 9](https://tomcat.apache.org/download-90.cgi)
### Eclipse EE
#### Eclipse setup server runtime
* Go to Window -> Preferences -> Server -> Runtime Environments
* Select **Add...**
* Choose **Apache Tomcat v9.0**
* Home Directory: browse to tomcat 9 folder location and select it
* Runtime JRE -> Alternate JRE: select jdk1.8

#### configure project in Eclipse
*  Right click on CourseManagementJDBCWebApp-> Build Path -> Configure Build Path...
* Remove JRE System Library
* Select **Add Library...**
* Select **JRE System Library**
* Choose **Alternate JRE** -> jdk1.8.

#### Eclipse setup server
* Window -> Show View -> select **Servers** (if you do not find this option in the menu, select **Other**, and type **Servers** into the Filter textbox. Then, select **Servers** ).

### NetBeans
#### NetBeans setup server runtime
* Go to Tools -> Servers ->
* Select **Add server...**
* Choose **Apache Tomcat or tomEE** name it 'tomcat 9'
* choose **Next**
* Server Location: browse to tomcat 9 folder location and select it
* choose **finish**
* after that select **platform** choose JavaPlatForm->jdk1.8

#### configure project in NetBeans 
* Right click on CourseManagementJDBCWebApp->Properties -> Build->Compile
* Choose JavaPlatForm->jdk1.8

#### add the server to the project in NetBeans
* Right click on CourseManagementJDBCWebApp->Properties->Run
* Choose Server:->tomcat 9

### Edit **persistence.xml** file in the project
* in the project structure go to src/main/java/META-INF/persistence.xml and change the properties value **javax.persistence.jdbc.user** and **javax.persistence.jdbc.password** to your username and password for mysql



## you can run the app on the server now


