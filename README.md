# Riot API와 Spark SQL을 활용한 TFT 티어 구간별 플레이 스타일 분석

## 1. 문제 정의

전략적 팀 전투(Teamfight Tactics, TFT)는 수많은 플레이어가 매일 경기를 진행하며 대량의 게임 데이터를 생성하는 게임이다. 본 프로젝트에서는 Riot Games에서 제공하는 TFT API를 활용하여 실제 경기 데이터를 수집하고, 플레이어 티어 구간에 따른 플레이 스타일 차이를 분석하고자 하였다.

특히 TFT는 크게 리롤덱, 운영덱으로 덱을 구분한다.

- 리롤덱 이란? 레벨업을 미루고 같은 챔피언을 반복적으로 구매하여 3성 챔피언을 만드는 전략
- 운영덱 이란? 골드와 체력을 효율적으로 관리하여 8~9레벨 이후 고코스트 챔피언을 활용하는 전략

본 프로젝트 에서는 아래와 같은 궁금점을 설정했다.

1. 리롤덱과 운영덱 중 어떤 전략이 더 높은 성적을 기록하는가?
2. 저티어(브론즈, 실버, 골드)구간과 상위권 티어(에메랄드, 다이아)구간의 리롤덱 운영덱 비율
3. 레벨에 따른 TOP4 비율

## 2. 시스템 아키텍처
본 프로젝트는 Riot TFT API를 통해 데이터를 수집 후, Hadoop HDFS와 Spark SQL을 활용하여 분석을 수행하였다.

데이터 처리 흐름

Riot TFT API

↓

Python 수집 프로그램

collect_matches.py (브론즈~골드), collect_matches2.py (에메랄드~다이아)

↓

CSV 파일 생성

tft_match_records.csv, tft_match_records2.csv

↓

HDFS 저장

↓

Spark SQL 분석

↓

결과 비교 및 인사이트 도출

# 사용기술: Python, Riot API, Hadoop HDFS, Spark SQL

## 3. 데이터 수집 방법
데이터 수집은 Riot API를 활용하여 진행

# 수집 대상
1. 하위권 티어(브, 실, 골)
2. 상위권 티어(에메, 다이아)

# 수집항목
* Match ID
* Tier (Bronze ~ Diamond)
* Division (1 ~ 4)
* Placement (순위)
* Level
* 사용 챔피언 정보
* 챔피언 몇성?
* 아이템

# 과정
1. Riot API를 통해 데이터 조회
2. Python으로 데이터 수집
3. CSV파일로 변환
4. HDFS 저장
5. Spark SQL 분석

# Data Scale
브, 실, 골 = 약 9400경기
에메, 다이아 = 약 6200경기

## AI Tool 사용 내역

- ChatGPT: README 구조 작성 및 프로젝트 기획 보조
