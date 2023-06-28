# 14장 가상메모리

# 연속 메모리 할당

프로세스에 연속적으로 메모리를 할당하는 방식

## 스와핑

---

메모리에서 사용하지 않는 일부 프로세스를 보조기억장치로 옮기고 실행할 프로세스를 메모리로 다시 옮기는 메모리 관리기법입니다. 

- 스왑 영역 ( Swap-space ) : 가상 메모리 관리를 위해 사용되는 디스크 영역, 프로세스들이 쫓겨나는 영역
- 스왑 인 ( Swap-in ) : 스왑 영역에 있던 프로세스를 다시 메모리로 옮기는 것
- 스왑 아웃 ( Swap-out ) : 메모리에서 프로세스를 스왑 영역으로 옮기는 것

![스와핑](https://private-user-images.githubusercontent.com/61916401/249511946-c7f130cd-fedb-42a3-8748-c0c2b097cf3c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTExOTQ2LWM3ZjEzMGNkLWZlZGItNDJhMy04NzQ4LWMwYzJiMDk3Y2YzYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yMGY4YmMyMTQzNTAzMmFiYzAzNzRkMzBjZWNkMWE0ZWVkMDk3ZDIyNGJmNmI0YjdkOTgzYjZhODBmMzY3NjRiJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.L9ZbUetuiapx0-Q3fA7yVeKBGECXH7xMKYcfEb1CrnE)


## 메모리 할당

---

메모리 공간에 프로세스를 연속적으로 할당하는 방법에는 대표적으로 최초 적합, 최적 적합, 최악적합이 있습니다.

![메모리 할당.png](https://private-user-images.githubusercontent.com/61916401/249511933-879bb449-bae4-4e0b-b304-5464f632d913.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTExOTMzLTg3OWJiNDQ5LWJhZTQtNGUwYi1iMzA0LTU0NjRmNjMyZDkxMy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1hYjY3MDZjZmFkZDA1ZDA3NDU1M2IyYjA2NzQwNjhiOWIwMzgxOTZiNTE4ZDVhODJjZDMxYTg3MDA3YWZmODlhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.96sKuvyMOo49rNoOxhYMDgqzz5GmjQA_lLp1ICB6j8c)

ex ) 20MB 에 프로세스를 메모리에 할당하는 과정

- 최초 적합

운영체제가 메모리 내의 빈 공간을 순서대로 검색하다가 프로세스를 적재할 수 있는 공간이 있으면 적재하는 방법입니다. 위 예에서는 A → B → C 순으로 탐색하다 공간 A 에 적재하게 됩니다.

- 최적 적합

운영체제가 메모리 내의 빈 공간을 모두 탐색 후 프로세스가 적재될 수 있는 가장 작은 공간에 적재하는 방법입니다. 위 예에서는 공간 C 에 적재하게 됩니다.

- 최악 적합

운영체제가 메모리 내의 빈 공간을 모두 탐색 후 프로세스가 적재될 수 있는 가장 큰 공간에 적재하는 방법입니다.

위 예에서는 공간 B에 적재하게 됩니다.

## 외부 단편화

---

프로세스가 메모리에 연속적으로 할당되는  환경에서 프로세스들이 실행과 종료되면서 생기는 메모리 사이사이 빈공간에 프로세스를 할당하기 어려운 공간으로 인해 메모리가 낭비되는 현상입니다.

![스크린샷 2023-06-25 오후 6.18.04.png](https://private-user-images.githubusercontent.com/61916401/249511954-dbd7cc50-92c4-4efc-9799-5e44d94a6683.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTExOTU0LWRiZDdjYzUwLTkyYzQtNGVmYy05Nzk5LTVlNDRkOTRhNjY4My5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kNjBiYzY5ZWI2MjBkOWExMDAxYjgzMTUwNDZmNWEzMTgwZGY5NmM0YTc0ODUyYWM4YjhiNTVjMGZlOTBiNWVlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.2fBKzR3SGH2OKFUlNGwOIxmA773owU48Qx4sGCRDzzg)

### 압축

---

외부 단편화를 해결하기 위한 대표적인 방법으로는 압축이 있습니다. 메모리에 흩어져 있는 프로세스를 재배치 하여 작은 빈공간을 하나의 큰 공간으로 만드는 방법입니다.

하지만 압축은 빈 공간을 하나로 만들기 위해 시스템이 하던일을 중지해야하고 내용을 옮기는 작업은 많은 오버헤드를 발생하기 때문에 적합한 방법은 아닙니다.

# 페이징을 통한 가상 메모리 관리

## 가상 메모리

---

실행하고자는 프로세스에 일부만 메모리에 적재하여 물리 메모리 크기보다 큰 프로세스를 실행할 수 있는 기법입니다.

![스크린샷 2023-06-25 오후 6.29.45.png](https://private-user-images.githubusercontent.com/61916401/249511960-6116c532-68ae-4bc6-b08b-eb1173fb57f3.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTExOTYwLTYxMTZjNTMyLTY4YWUtNGJjNi1iMDhiLWViMTE3M2ZiNTdmMy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iMGU3YWY1MjFiNzZkNjZhZWUwOTFkMzY0MzUxNWNkZDE5ODllNTI5MGIzOWU1MWIyZTQ5ZTljNGJjZTRmOTMxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.lZAYKsEYqgfBIFvFHTACny7v6Gjz1PL7LKPiKCqLKC0)

가상 메모리 기법에는 크게 페이징과 세그멘테이션이 있습니다.

## 페이징

---

프로세스의 논리 주소 공간을 페이지 라는 일정한 단위로 자르고, 메로리 물리 주소 공간을 프레임 이라는 페이지와 동일한 크기의 단위로 자른 뒤 페이지를 프레임에 할당하는 가상 메모리 기법입니다.

예를 보면 프로세스 B는 메모리에 연속적으로 할당되지 않고 불연속적으로 할당되어 외부 단편화가 발생하지 않았습니다.

![스크린샷 2023-06-25 오후 6.37.06.png](https://private-user-images.githubusercontent.com/61916401/249512307-306406d1-4c9d-4afc-b8d8-88cddffb9707.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzA3LTMwNjQwNmQxLTRjOWQtNGFmYy1iOGQ4LTg4Y2RkZmZiOTcwNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05Mjg4NTBhN2RjZWNhYmMyZjM1YjNjNTk1NjI5OGY4NzU0NmNkZWFjMjIzYjM3ZjA3ZjAxYzYzYTg5NmMyZTZkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.F_OqI5YmUQeno7F0TbHgm-Pt_vC1GpOAKybjp_-kOG8)

페이징에서도 스와핑 기법을 사용할 수 있습니다. 여기서 스와핑은 프로세스 전체가 아닌 페이지 단위로 스왑 인(페이지 인)/스압 아웃(페이지 아웃)이 됩니다. 메모리에 적재될 필요가 없는 페이지는 스왑 아웃이 되고 실행에 필요한 페이지는 스왑 인됩니다.

따라서 프로세스를 실행하기 위해 프로세스 전체가 메모리에 적재될 필요가 없습니다. 프로세스 페이지 중 실행에 필요한 페이지만 메모리에 적재하고 나머지는 보조기억장치에 넣어둘 수 있습니다. ⇒ 메모리보다 더 큰 프로세스를 실행할 수 있음

## 페이지 테이블

---

프로세스가 메모리에 불연속적으로 있다면 CPU는 프로세스를 순차적으로 실행할 수 없습니다. CPU가 프로세스 프레임에 모든 위치를 알고 있기는 어렵기 때문입니다. 

따라서 논리 주소에는 연속적으로 배치되도록 페이지 테이블을 사용합니다.

![스크린샷 2023-06-25 오후 6.50.00.png](https://private-user-images.githubusercontent.com/61916401/249512318-f19ac13a-906f-4e24-8098-697cf9c8b73f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzE4LWYxOWFjMTNhLTkwNmYtNGUyNC04MDk4LTY5N2NmOWM4YjczZi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wNjFkYmJmNzkyNWUxZmRlNDZmZjM2ZTI4ZTdlNzFkYzc4OTI0MWQ4MTc0ODBlMTQ3NWRkY2UxNWQ3N2M3YmVkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.t0E0qHZBP3SA1qvpctd2iAzWAATfwjLIhtK2MPCkNh0)

위와 같이 페이지 테이블을 사용하면 물리 주소상으로는 프로세스들이 분산되어 적재되어있지만 논리 주소는 연속적으로 사용가능하여 CPU는 논리 주소를 사용하여 실행할 수 있습니다.

### 내부 단편화

---

모든 프로세스의 크기가 페이지 크기의 배수가 아닙니다. 따라서 마지막 페이지는 프레임에 적재시 메모리 크기가 남습니다. 이러한 경우를 내부 단편화라고 합니다. 페이지 크기를 작게 설정하면 해결할 수 있지 않을까 생각할 수 있지만 이는 페이지 테이블 크기가 커지기 때문에 페이지 테이블이 차지하는 공간이 낭비됩니다.

### 페이지 테이블 베이스 레지스터 ( PTBR )

---

CPU내의 있고 각 프로세스의 페이지 테이블이 적재된 주소를 가지고 있습니다.

프로세스 A가 실행될 때 PTBR은 메모리에 있는 페이지 테이블에 접근하고 이를 통해 프로세스 A의 페이지가 적대된 프레임을 알 수 있습니다.

하지만 이런식은 페이지 테이블을 접근하고 이를 통해 프레임에 접근합니다. 총 두 번의 메모리 접근이 필요하기 때문에 메모리 접근 시간이 두 배로 증가합니다. 

**TLB**

---

이를 해결하기 위해 CPU 곁에 ( 일반적으로는 MMU 내에 존재함 ) TLB 라는 페이지 테이블의 캐시 메모리를 둡니다. 이는 참조 지역성에 근거해 주로 최근에 사용된 페이지 위주로 가져와 저장합니다.

TLB 히트 : CPU가 발생한 논리 주소에 대한 페이지 번호를 TLB가 가지고 있는 경우

TLB 미스 : CPU가 발생한 논리 주소에 대한 페이지 번호를 TLB가 가지고 있지 않아 메모리 내의 페이지 테이블에 접근해야하는 경우

![스크린샷 2023-06-25 오후 7.12.31.png](https://private-user-images.githubusercontent.com/61916401/249512324-00c9cfc6-6c10-489d-a5fe-f255aba6906e.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzI0LTAwYzljZmM2LTZjMTAtNDg5ZC1hNWZlLWYyNTVhYmE2OTA2ZS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02MTE1NGJmNjU2Mzg3NzVhY2I4ZDhjOTgzZDI0OGY1ZmJhMWFiOTBmYzQ3NjgyNDU3ZWZlNGExM2ExMjZhM2Y0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.TtKZTRSg9FBjeRKhWfUW7o2acFo9AahC0fOxtuQz4SY)

### 페이징에서의 주소 변환

---

하나의 페이지 혹은 프레임은 여러 주소를 포괄하고 있습니다. 따라서 특정 주소에 접근하려면 두 가지 정보가 필요합니다.

- 어떤 페이지 혹은 프레임에 접근하고 싶은지
- 접근하려는 주소가 그 페이지 혹은 프레임으로부터 얼마나 떨어져 있는지

![스크린샷 2023-06-25 오후 7.14.18.png](https://private-user-images.githubusercontent.com/61916401/249512331-d78ecd8b-cd35-4148-a54a-5ec143ddba60.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzMxLWQ3OGVjZDhiLWNkMzUtNDE0OC1hNTRhLTVlYzE0M2RkYmE2MC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jMTgyYjhiMTZlMTQ0YzMzMWVlOGVjZjdkZmEwNzE1NjdlOTFiODJmNmQxMmNiNTkwNDM4MGM3MDA4ZmVmZWZkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.STRITrJ9X_ODF4IzjZHt3hyTKPyr8ITIjS2cT_yJulc)

따라서 페이징 시스템에서 모든 논리 주소는 기본적으로 페이지 번호와 변위를 사용

![스크린샷 2023-06-25 오후 7.15.26.png](https://private-user-images.githubusercontent.com/61916401/249512338-28cbb8d8-a2b0-4cac-9cab-4c562da53eff.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzM4LTI4Y2JiOGQ4LWEyYjAtNGNhYy05Y2FiLTRjNTYyZGE1M2VmZi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1jZDUxZDc4MzdmZThmYTkwMTZiZTQyOTNhY2Q1OTM5ZDJiZTQ5ZTJmNTkxMzQwMGY4N2RhZDk3ZjE1N2M1NjNhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.AwDUtclyDXPab7M3V-uiKJlIKxavpnYK_ssBpxUmu38)

페이지 번호 : 접근하려고 하는 페이지 번호

변위 : 접근하려는 주소가 프레임의 시작 번지로 부터 얼만큼 떨어진지에 대한 정보

![스크린샷 2023-06-25 오후 7.19.45.png](https://private-user-images.githubusercontent.com/61916401/249512346-eb44f160-21b7-48a9-8fd7-9ea96dcf70f2.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzQ2LWViNDRmMTYwLTIxYjctNDhhOS04ZmQ3LTllYTk2ZGNmNzBmMi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03MTg3NmZiOTE3N2M4NjcwY2YwNWFjZDYxYmNmNDYzOGI5NzgyNjQwZDk5YzdkYThlMWVmMWZjMGJmM2Q4MzUxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.YGnT1VtQ-oQcI4QQ_2WdIs6uRJb8m4Fqc1Yvpyyxpus)

### 페이지 테이블 엔트리

---

페이지 테이블의 각 행들을 페이지 테이블 엔트리라 합니다. 여기에는 앞서 말한 페이지 번호, 프레임 번호만 있는 것이 아닌 다른 중요한 정보들도 있습니다.

대표적으로는 유효비트, 보호비트, 참조비트, 수정비트 입니다.

**유효비트**

---

현재 해당 페이지에 접근 가능 여부를 알려줍니다. 모든 페이지가 메모리에 적재되어있는 것은 아니기 때문 ( 스와핑으로 인해 일부 페이지는 스왑 영역에 있을 수 있음 )

- 유효 비트가 1 이면 현재 메모리에 적재되어 있는 페이지
- 유효 비트가 0 이면 현재 메모리에 적대되어 있지 않는 페이지

<aside>
💡 페이지 폴트

메모리에 적재되어 있는 않은 페이지를 접근하려고 하는 경우 발생, 페이지 폴트는 다음과 같이 처리된다. ( 하드웨어 인터럽트와 유사 )

1. CPU는 기존의 작업 내역을 백업한다.
2. 페이지 폴트 처리 루틴을 실행한다.
3. 페이지 처리 루틴은 원하는 페이지를 메모리로 가져온 뒤 유효 비트를 1로 변경한다.
4. 페이지 폴트를 처리했다면 이제 CPU는 해당 페이지에 접근할 수 있음
</aside>

**보호 비트**

---

페이지 보호 기능을 위한 비트, 해당 비트를 통해 페이지가 읽고 쓰기가 모두 가능한 페이지인지, 혹은 읽기만 가능한 페이지인지를 확인 가능 → 접근 권한 비트라고도 함

- 읽고 쓰기가 모두 가능인 경우 1
- 읽기 전용인 경우 0

보호 비트는 읽기, 쓰기, 실행으로 세게의 비트로도 구성가능 ex ) 100 읽기전용, 110 읽고 쓰기 가능, 111 읽기, 쓰기 ,실행 가능

**참조 비트**

---

CPU가 해당 페이지에 접근 여부

적재 이후 CPU가 읽거나 쓴 페이지는 참조 비트가 1로 저장, 한 번도 읽거나 쓴 적이 없는 페이지는 0으로 유지됩니다.

**수정 비트**

---

해당 페이지에 데이터를 쓴 적이 있는지 없는지 수정 여부 *더티 비트 라고도 부름

- 변경된 적이 있다면 1
- 변경된 적이 없다면 0

<aside>
💡 수정 비트가 필요한 이유
CPU는 메모리를 읽기도 하지만 메모리에 값을 쓰기도 합니다. CPU가 한 번도 접근하지 않았거나 읽기만 한 페이지의 경우 스왑 영역에 내용과 메모리에 내용이 동일합니다. 하지만 쓰기 작업을 수행한 페이지 (수정 비트가 1인 페이지)의 경우 스왑 영역에 내용과 서로 다른 값을 갖기 때문에 스왑 아웃 이후 변경된 값을 스왑 영역에 기록하는 작업이 추가로 필요하다.

</aside>

### 페이징의 이점 - 쓰기 시 복사

---

프로세스 간 페이지 공유

프로세스 fork 시스템을 호출하면 부모 프로세스의 복사본이 자식 프로세스로 만들어집니다. ‘프로세스 간에는 기본적으로 자원을 공유하지 않는다.’ 는 프로세스의 전통적인 개념에 따라 부모와 자식 프로세스는 적재된 메모리는 서로 다른 메모리 공간에 생성됩니다. 

![스크린샷 2023-06-25 오후 9.30.42.png](https://private-user-images.githubusercontent.com/61916401/249512350-28040587-ca44-4e7f-8939-e9578806b586.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzUwLTI4MDQwNTg3LWNhNDQtNGU3Zi04OTM5LWU5NTc4ODA2YjU4Ni5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kMTcxMGQ4MzFhODJkYzM3ODhlNWFiNDU4YTJhZTk4ODQ2ZmFkMmIzZGI0MzUyY2Q1ZWJkNWMwYWFkOWI2YTliJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.34em1PNAC-Zy-oP8WNGkbubLpeA-OWz3WUgXpa6qNik)

쓰기 시 복사에서는 부모 프로세스와 자식 프로세스가 동일한 프레임을 가리킵니다. 여기서 부모와 자식 프로세스가 메모리에 어떠한 데이터도 쓰지 않고 읽기 작업만 한다면 같은 상태가 지속됩니다.

하지만 프로세스 간에는 자원을 공유하지 않기 때문에 부모나 자식 프로세스 중 하나가 페이지에 쓰기 작업을 사용한다면, 해당 페이지가 별도의 공간으로 복제됩니다. 

![스크린샷 2023-06-25 오후 9.39.27.png](https://private-user-images.githubusercontent.com/61916401/249512355-15dd665f-9540-45b5-a184-f177d36dce3d.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyMTE2LCJuYmYiOjE2ODc5NjE4MTYsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTEyMzU1LTE1ZGQ2NjVmLTk1NDAtNDViNS1hMTg0LWYxNzdkMzZkY2UzZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDE2NTZaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02ZjM5NWUzNjcyZGQ3NjA1Y2U1NjgxM2Q3YTk3MTUwNGQxNjhiN2NlYjI4YmU3YjYwMzgxYmZmZjI0MTk5NThmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.jSTzjgCnXJKYT1mfO9Xh66pcRJwu41m5NEZ2xiI52D0)

### 계층적 페이징

---

![스크린샷 2023-06-27 오후 11.55.28.png](https://private-user-images.githubusercontent.com/61916401/249516450-cb02269e-6ded-48a2-b7b2-e8f0ad1fd226.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDUwLWNiMDIyNjllLTZkZWQtNDhhMi1iN2IyLWU4ZjBhZDFmZDIyNi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02Y2UyYzVjNmU0NDAxZWIxNjgxZWY2MDlmNjAxMTdhY2U1NWRhMjg3YWJmMTc2MGQ3NjUwYmFmYWU2ZDYwYTRiJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.-0ygQvpckqS-ump2ssG4slBAGu3X9O8pbseE1ZO3zrY)

기존 페이지 테이블을 여러 개의 페이지로 나누어 이 페이지를 가리키는 페이지 테이블(outer 페이지 테이블)을 투는 방식입니다.

계층적으로 구성하면 페이지 테이블을 스왑 아웃하여 사용할 수 있고 필요한 경우 스왑인 하여 참조할 수 있습니다.

> CPU와 가장 가까이 위치한 페이지 테이블(Outer 페이지 테이블)은 항상 메모리에 유지해야 합니다.
> 

계층적 페이지 테이블에서 사용하는 논리 주소

---

![스크린샷 2023-06-28 오전 12.08.09.png](https://private-user-images.githubusercontent.com/61916401/249516452-9e00876a-893d-41b4-847c-77fe5cff0615.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDUyLTllMDA4NzZhLTg5M2QtNDFiNC04NDdjLTc3ZmU1Y2ZmMDYxNS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iZjU2YzhlMGQxZGRiZjcwN2M0ODk0MWE5YTdjMDAzZGZlY2IyZWJlNmE0NzE4ZjcyZmU1MDkyMzIxZjMzNjgyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.YcdvSociVykzRWWNEdO-2Cp8fvgXMHFi-vHszn5kS0k)

- 바깥 페이지 번호 : CPU와 근접한 곳에 위치한 페이지 테이블 엔트리
- 안쪽 페이지 번호 : 페이지 테이블의 페이지 번호

주소 변환 과정

---

![스크린샷 2023-06-28 오전 12.09.45.png](https://private-user-images.githubusercontent.com/61916401/249516456-4524c4dd-fadf-4f48-80fe-fe2536ca8c5c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDU2LTQ1MjRjNGRkLWZhZGYtNGY0OC04MGZlLWZlMjUzNmNhOGM1Yy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yNGU5NzQzMmU1OWFiZjBmYTRkZTFiODY2NzRhMDY0MGFmNzFkN2E2YzBiODgwNDlkYzc3Zjg4MDI2Nzg5NmQ0JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.ITZEGECeZdp_91AZ-tCCiWLe4G79DctrsvkyLMimsYw)

1. 바깥 페이지 번호를 통해 ‘페이지 테이블의 페이지’를 찾기
2. ‘페이지 테이블의 페이지’를 통해 프레임 번호를 찾고 변위를 더함으로서 물리 주소 얻기

# 페이지 교체와 프레임 할당

---

운영체제는 프로세스들이 한정된 메모리를 효율적으로 이용하기 위해 다음 두 가지를 만족해야 합니다.

- 기존에 적재된 불필요한 페이지를 선별해 보조기억장치로 내보내기
- 프로세스들에게 적절한 수의 프레임 할당하기

## 요구 페이징

---

프로세스를 메모리에 적재할 때 필요한 페이지만 메모리에 적재하는 기법, 요구 페이징 기법 처리 과정

1. CPU가 특정 페이지에 접근하는 명령어를 실행한다.
2. 해당 페이지가 현재 메모리에 있을 경우 (유효 비트가 1일 경우 ) CPU는 페이지가 적재된 프레임에 접근한다.
3. 해당 페이지가 현재 메모리에 없을 경우 (유효 비트가 0일 경우 ) 페이지 폴트가 발생한다.
4. 페이지 폴트 처리 루틴은 해당 페이지를 메모리로 적재하고 유효 비트를 1로 설정한다.
5. 다시 1번을 수행한다.

 

### 순수 요구 페이징

---

메모리에 아무런 페이지도 적재하지 않은 경우 무작정 실행부터 할 수 있습니다. 이러한 경우 첫 명령어를 실행하는 순간 부터 페이지 폴트가 발생하고, 실행에 필요한 페이지가 어느 정도 적재된 후에는 페이지 폴트 발생 빈도가 떨어집니다. 이를 순수 요구 페이징 기법입니다.

요구 페이징 시스템이 안정적으로 작동하려면 아래 두 가지를 충족해야 합니다.

- 페이지 교체
- 프레임 할당

# 페이지 교체 알고리즘

---

실행에 필요한 페이지는 메모리에 올릴 때 빈 프레임 없는 경우 메모리에 적재된 페이지를 보조기억장치를 보내기 스압 아웃할 페이지를 선택하는 알고리즘입니다.

여기서 좋은 페이지 교체 알고리즘은 페이지 폴트가 적게 발생하는 알고리즘입니다.

따라서 페이지 폴트 횟수를 알아야하고 해당 횟수는 페이지 참조열로 부터 확인할 수 있습니다.

`2 2 2 3 5 5 5 3 3 7`

위의 순서로 페이지 를 접근 하였을 때 연속된 페이지를 생략하면 페이지 참조열이 됩니다.

`2 3 5 3 7`

연속된 페이지는 페이지 폴트가 발생하지 않기 때문에 생략합니다.

## FIFO 페이지 교체 알고리즘

---

가장 먼저 들어온 페이지 부터 교체하는 알고리즘입니다.

![스크린샷 2023-06-26 오후 11.25.05.png](https://private-user-images.githubusercontent.com/61916401/249516426-a3c6cfe9-b978-4b5e-876f-a1ec71fc3e9f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDI2LWEzYzZjZmU5LWI5NzgtNGI1ZS04NzZmLWExZWM3MWZjM2U5Zi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0zMmM3M2NhNmEyOGY2NmIyOTgyMzgwYWU0ZTljNzkyOWQ3OTVlMzczMjMxMjdiNTViZTc3ZWViMTExNGUxZGUxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.E5E_Bekt_1fWrkAoheYW55g398CJaR7EtvXfws5ftIU)

프로그램 실행 초기에만 잠깐 사용되는 페이지에 대해서는 좋은 알고리즘이지만 프로그램 실행 동안 계속 사용해야하는 내용에 대해서는 좋지 않은 알고리즘입니다.

### 2차 기회 페이지 알고리즘

---

FIFO 페이지 교체 알고리즘을 변형한 알고리즘입니다. 참조 비트를 추가하여 참조 비트가 1인 경우 0으로 교체한뒤 적재 시간을 현재 시간으로 변경하여 1번의 기회를 더 주는 알고리즘 입니다.

참조 비트가 0인 경우에는 바로 페이지 교체가 발생합니다.

## 최적 페이지 교체 알고리즘

---

CPU의 참조되는 횟수를 기준으로 페이지를 교체하는 알고리즘입니다.

사용빈도가 높은 페이지는 메모리에 남기고 사용빈도가 낮은 페이지를 교체하는 알고리즘 입니다.

![스크린샷 2023-06-26 오후 11.30.40.png](https://private-user-images.githubusercontent.com/61916401/249516431-994de084-7a64-4f80-bf6e-bf7b4215bb45.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDMxLTk5NGRlMDg0LTdhNjQtNGY4MC1iZjZlLWJmN2I0MjE1YmI0NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02ODU2MzFhMzg5Y2MzZjU3ZDdlNmFlMjg3NjQ5MTM4YWIxNWZiNTJmOGVkNDY0YTQ3OWNlZjU3OWQzMDI3ODZlJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.PYsZpXsjecWqDLO-3DHjZmQfI8AGnJ6XA0pINHgyfO8)

가장 낮은 페이지 폴트를 보장하는 알고리즘이지만 실제 구현이 어려운 알고리즘으로 주로 다른 페이지 교체 알고리즘의 이론상 성능을 평가하기 위해 사용됩니다.

## LRU 페이지 교체 알고리즘

---

가장 오랫동안 사용하지 않은 페이지를 교체하는 알고리즘입니다.

![스크린샷 2023-06-26 오후 11.33.13.png](https://private-user-images.githubusercontent.com/61916401/249516434-7a1c70a8-565d-4863-8e21-275f3fd9a2dd.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDM0LTdhMWM3MGE4LTU2NWQtNDg2My04ZTIxLTI3NWYzZmQ5YTJkZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1kM2IyMzQ2N2Q4M2NiZjNiMzg4NzRkZjM2ZmY0NWM3MjUzYmVlN2FmNDliMTNiODk1ZGJiNjhlZjQ0NmI5ZWNhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.NdDmS5vAzjoReEE3PX6sw3ocZWBsVqbpVnm5p74kjQo)

# 스레싱과 프레임 할당

---

페이지 폴트가 자주 발생하는 원인에는 나쁜 페이지 교체 알고리즘만 있는 것이 아닙니다.

프로세스가 사용할 수 있는 프레임 수가 적은 경우 페이지 폴트가 자주 발생합니다. 이런 경우 스레싱이 발생할 수 있습니다.

- 스레싱 : 빈번한 페이지 교체로 인해 CPU이용률이 낮아지는 문제

![스크린샷 2023-06-27 오후 10.16.34.png](https://private-user-images.githubusercontent.com/61916401/249516439-3106589e-4874-4202-b8cf-ea4dfa07277b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDM5LTMxMDY1ODllLTQ4NzQtNDIwMi1iOGNmLWVhNGRmYTA3Mjc3Yi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lZGEyZjgxNjEwNWNkNGZhYjA4ZjI4YTdiNjUwNTVlNWFkNjhkZTZjYTdkNjRhZDRlNWVlZDMzMmNjYzNhOWEyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.rVahKCZDm7CF5fodNUvaakTQwzA-hAYHcEpiCdN_Q6E)

![스크린샷 2023-06-27 오후 10.19.20.png](https://private-user-images.githubusercontent.com/61916401/249516443-d41a39a9-b836-4510-8e54-4abfe27c7095.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDQzLWQ0MWEzOWE5LWI4MzYtNDUxMC04ZTU0LTRhYmZlMjdjNzA5NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT00YTEzYjc1OWQ2MmM3ZDE3YjZjNGY2NWZiOGVmNTMxNDJiMWJlNjg2YTRkNThlNGNjYjY2MWMzNzhmODMzZGVkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.EijEUg0DX6qs1aPvsRrsFk0q1e6NTpEyG_UeNifsghQ)

ex) 스레싱을 그래프로 표현

- 멀티프로그래밍의 정도 : 메모리에 동시 실행되는 프로세스의 수

위의 그래프는 동시에 실행되는 프로세스의 수를 늘린다고 해서 무조건 CPU 이용률이 좋아지는 것은 아님을 나타냅니다.

스레싱이 발생하지 않기 위해서는 각 프로세스가 필요로 하는 최소 프레임 수가 보장되어야 합니다.

방법으로는 프레임 할당 방식이 있습니다. 이는 정적 할당 방식과 동적 할당 방식으로 나뉘어 집니다.

### 정적 할당 방식

---

- 균등 할당 : 모든 프로세스에 동일한 프로세스를 할당합니다.
- 비례 할당 : 프로세스 크기에 비례하여 프로세스를 할당합니다.

### 동적 할당 방식

---

- 작업 집합 모델 : 실행 중인 프로세스가 일정 시간 동안 참조한 페이지의 집합을 만들고 해당 크기 만큼 프레임을 할당합니다.

![스크린샷 2023-06-27 오후 10.42.21.png](https://private-user-images.githubusercontent.com/61916401/249516447-315cdaa2-60da-4e88-9f5d-910e7cee697c.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDQ3LTMxNWNkYWEyLTYwZGEtNGU4OC05ZjVkLTkxMGU3Y2VlNjk3Yy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wYjYwZTU5YmI2M2ViNTZkNmEyMzNmOTM5MTUyZDY4ODZlY2EzZmJmZmMyYjdmNjBlNTJhZjA3NGZiZmIzYmViJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.UGdrxl0oO0faFkQYt37J1-jUDXNwOvfFySV5tcjtqX8)

> 작업 집합 : { 5, 6, 7 } 최소 3개의 프레임이 필요
> 

- 페이지 폴트 빈도 : 페이지 폴트율 상한선과 하한선을 정하고 그에 따라 프레임을 더 할당하거나 회수합니다.

![스크린샷 2023-06-27 오후 10.40.20.png](https://private-user-images.githubusercontent.com/61916401/249516446-7770227a-8860-4756-8ab6-d55bffcb9ced.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJrZXkiOiJrZXkxIiwiZXhwIjoxNjg3OTYyOTI4LCJuYmYiOjE2ODc5NjI2MjgsInBhdGgiOiIvNjE5MTY0MDEvMjQ5NTE2NDQ2LTc3NzAyMjdhLTg4NjAtNDc1Ni04YWI2LWQ1NWJmZmNiOWNlZC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBSVdOSllBWDRDU1ZFSDUzQSUyRjIwMjMwNjI4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDIzMDYyOFQxNDMwMjhaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT00YzMyZWI3NTcyMWJiNjljODg4ZWU0MWQwOGRhZmI1M2E0NDllNTk5YjViMGI4YzQ0ODFkYzI2NDIzOTFhM2Q3JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.Pz6WhKEjEtBa32yQ5l1NTe6Px6F7z8tbCpBnzxIpyIQ)