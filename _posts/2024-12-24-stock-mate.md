---
layout: post
title: Stock Mate
subtitle: Warehouse Management System
author: Insung
categories: Project
banner:
  video: https://github.com/user-attachments/assets/a35cc1ae-2eb4-43e0-89c6-f0daba9a7e5d
  loop: true
  volume: 0.8
  start_at: 8.5
  image: assets/images/stockmate-thumbnail.jpeg
  opacity: 0.618
  background: "#000"
  height: "100vh"
  min_height: "38vh"
  heading_style: "font-size: 4.25em; font-weight: bold; text-decoration: underline"
  subheading_style: "color: gold"
tags: [project]
top:
sidebar: []
---

## Stock Mate - WMS (Warehouse Management System)

## 프로젝트 소개

**Stock Mate**는 창고 관리 시스템(WMS)으로, 재고 관리 및 입출고 처리를 더욱 효율적으로 관리할 수 있도록 다양한 기술을 도입하였습니다. 특히, **OCR (Optical Character Recognition)** 기술을 활용하여 데이터 입력과 처리를 자동화하고, 재고 관리의 **정확도**를 **크게 향상**시켰습니다.

## 프로젝트 기능

### 1. **OCR 기술 도입**
**OCR** 기술을 통해 재고 관리 및 입출고 처리의 **효율성**을 크게 개선하였습니다. 기존의 수동 데이터 입력 방식을 개선하여 **실시간**으로 데이터가 정확하게 반영되며, 오류를 최소화할 수 있었습니다.

#### 주요 성과:
- **입출고 처리 시간 단축**:  
  기존 5분에서 1분으로 입출고 처리 시간을 **80% 단축**하였습니다.
  
- **재고 정확도 향상**:  
  수동 데이터 입력 및 오류로 인해 재고 정확도가 90%였으나, OCR 기술 도입 후 **99.9%**로 **향상**되었습니다.
  
- **입출고 오류 감소**:  
  기존 방식에서 발생하던 입출고 오류가 **90% 감소**하였습니다.

- **재고 관리 실시간 반영**:  
  기존에는 재고 현황을 반영하는 데 2시간 이상 소요되었으나, OCR 스캔 후 **즉시** 데이터베이스에 반영되어 현재 **가용 수량**을 정확히 파악할 수 있게 되었습니다.

### 2. **공간 효율성 극대화**

**바코드** 및 **QR 코드** 이미지를 최초 생성 후, 해당 이미지의 저장 경로만을 데이터베이스에 기록함으로써 중복 저장을 방지하고, 저장 공간을 효율적으로 **최적화**했습니다.

#### 주요 성과:

- **중복 저장 방지**:  
  **바코드** 및 **QR 코드** 이미지 생성 시, 이미지가 처음 생성되지 않았다면 뷰 페이지에서 이미지 **생성 버튼**을 통해 이미지를 생성할 수 있도록 하며, 이후 이미 생성된 이미지는 추가로 생성되지 않도록 **다운로드 버튼**만 활성화하여 중복 생성 및 저장을 방지했습니다. 이를 통해 불필요한 이미지 생성 및 저장을 막고, 시스템 **효율성**을 **향상**시켰습니다.

- **저장 공간 절감**:  
  이미지 파일을 매번 데이터베이스에 직접 저장하던 기존 시스템에서, 이미지 경로만 저장하도록 변경하여, 전체 시스템의 저장 공간을  **약 30% 절감**하는 성과를 달성하였습니다.


## 사용된 기술 스택

### Programming Language

---
<a href="https://www.java.com" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" alt="java" width="40" height="40"/>
</a><br><br>

### Frontend

---
<a href="https://www.w3.org/html/" target="_blank" rel="noreferrer"> 
  <img style="float:left; margin-right:5px;" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="40" height="40"/>
</a>
<a href="https://www.w3schools.com/css/" target="_blank" rel="noreferrer"> 
  <img style="float:left; margin-right:5px;" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" alt="css3" width="40" height="40"/>
</a> 
<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript" target="_blank" rel="noreferrer"> 
  <img style="float:left; margin-right:8px;" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript" width="40" height="40"/>
</a>
<a href="https://jquery.com/" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FF0Hil%2FbtsDqQe9Gh9%2FgEqI1NbhRoCPSWh4v4Vprk%2Fimg.png" alt="jquery" width="40" height="40"/>
</a>
<a href="https://www.w3schools.com/xml/ajax_intro.asp" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fd0BpMb%2FbtsDxNgClLV%2FHWQNqIZDFIFVhaiEGk3o1k%2Fimg.png" alt="ajax" width="40" height="40"/>
</a><br><br>

### Backend

---
<a href="https://spring.io/" target="_blank" rel="noreferrer"> 
  <img style="float:left; margin-right:7px;" src="https://www.vectorlogo.zone/logos/springio/springio-icon.svg" alt="spring" width="40" height="40"/>
</a>
<a href="https://blog.mybatis.org" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdeIusJ%2FbtsDrFc1hLD%2FYkTAFHVyXRKm9GiTlvSwzk%2Fimg.png" alt="mybatis" width="40" height="40">
</a><br><br>

### Database

---
<a href="https://www.mysql.com/" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmMHpU%2FbtsDxLXpqlY%2FIUikfxyNVo3YXbl2K5QndK%2Fimg.png" alt="mysql" width="40" height="40"/>
</a><br><br>

### Deployment Tools

---

<a href="https://git-scm.com/" target="_blank" rel="noreferrer"> 
  <img style="float:left; margin-right:5px;" src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/>
</a> 
<a href="https://github.com/" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbxixOB%2FbtsDrkG3rTF%2Fd7wMGaUhBtJ7srWtBuGaxk%2Fimg.png" alt="github" width="40" height="40"/>
</a>
<a href="https://tomcat.apache.org/" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&amp;fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrbPBh%2FbtsDqnqHRBc%2FKsGY3yKAJS4EAIWm5gjMik%2Fimg.png" alt="tomcat" width="40" height="40"/>
</a>
<a href="https://www.docker.com/" target="_blank" rel="noreferrer">
  <img style="float:left; margin-right:5px;" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/docker/docker-original-wordmark.svg" alt="docker" width="40" height="40"/>
</a>
<a href="https://postman.com" target="_blank" rel="noreferrer"> 
  <img style="float:left; margin-right:5px;" src="https://www.vectorlogo.zone/logos/getpostman/getpostman-icon.svg" alt="postman" width="40" height="40"/>
</a>
<br><br>

## 로그인 정보

- **Email**: example@manager.com
- **Password**: 1234

## 프로젝트 링크  
**URL:** <a href="http://c7d2408t1p1.itwillbs.com" target="_blank" rel="noreferrer">Stock Mate</a>

**Github:** <a href="https://github.com/in27sung/stock-mate" target="_blank" ref="noreferrer">Source code</a>
