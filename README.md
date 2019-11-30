# ����� �� ��������� �������

## (��������� � ��������� ������)

### ������� ������:

`�������� ���������, ������� ������ ����������� �������������� ������ �� ��������� ����. ���� � �������� ��� ��������� �� ��������� ��������� ����� ������ ����������.`

## ������������� �����:
#### ������ �����������:
* ***����������� �������������� ������ (AST)*** - ������ ������������� ����������� �������������� ��������� ��������� ����, ����������� �� ����� ����������������. ������ ���� ������ ���������� �����������, ������������� � �������� ����.
* ***�������� ��������*** - ����� ��������, ��� �������������� ��� �������������� �������, ����� ��� ������� ��� ���� ������, ���������� � �������� ���� �����.
* ***����������*** - ����� ������ ��� �������������� �����.
* ***����������-��������� ����������*** - ������������ ��� ���������� ����������: ����� ������ ������������, ������� ��������� ��� ��������� ������ � ������ ���������� �����. ������� ������������ - ������� ������.
* ***������������ �������*** - ������������ ������� �����, ������������ ���������� �����������.
* ***�������������� �������*** - ��������� �������, ������������ �������� ������������ �������� � ������������ � ��������� ������������.

#### �������� ������� � �������:
##### 1. ����� ������������ ������.
����� ������������ ������ - �������� ����������� ��������������� �������, ����������� ���� ��������� ������ ��������, ��� ������ ��������� ������������� ������ �� ������ ����������-��������� ����������. ���������� ������ ���������������, �����-������� ��������� ������, ���������� �� ������������ �����������. \
������ ����� ����� ��� �������� ����������: 
| |  ��������������� ������  |  ������ � ��������� |
|-| :------------------------ | :------------------- |
|�����������| ��� �������� ����� ���� ����� `LL(k)` ����������, ����������� �� ���������� ������ ��� ������� ���������� ������� ���� �� �������������� ��������� ��������� ������� �����������| ������ ������������ ������ ������ �������� ��������� ��� �������������� �������� ������ �� �������, ���� ���� �� ������� �� ���������� �������  |
|�������� ���� ���������| 1) ���������� ��������� ��������� ��������� ������ �� �������� ������ � ����� ������� ������ �� �����;  2) ���� ������� ���������, ����������� �� � ������������ �� ��� 1;  3) ���������� � ������� ��������������� �������, ��������, ����� ������� �� ���������� ���������� ��������� � ��������� �� ��� 1. | 1) ���������������� �������� ������� ������ �����-�������;  2) ��������� ������ ������� ������ �������� ���������� ��� ������ ����� �� ������ ������ ������ ������ ��� ������ �������� �����������;  3) ������������ ������� ������� ������ � ������ ����� ������� �������� �������������;  4) ����������� ����������� � ������ ����� ���������� ��������� ���� �� �������.|
|���������| ***O(n)***  | �� ***O(<nobr>*2*^n</nobr>)*** |
##### 2. �������������� ���������� �����������.
���������� ������ �� ����� ������������ ������ ��������. \
���� �������������� ���������� ��������� �� ��������� ��� ���������: <, >, = 
* `a < b` - ��������, ��� � ��������� ��������� b. 
* `a > b` - ��������, ��� � ������ ��������� ��� b. 
* `a = b` - ��������, ��� � ������ ��������� ��� b. 

�� ��� �������� ������� ��������� ���������� ��������� ��� ������ ����������. ����������� ���� ������� ����� ��, ��� ���� � ��� ���� n ����������, �� ������ ������� ����� ***nxn***, � ���������  �� ������ - ***O(<nobr>*n*^2</nobr>)***.

��������:
1) ������� ������ �� ������� ������ � �������� ��� � ����.
2) �������� ��������� ������ �� ������� ������ � ������ �������� �����: ���� ��������� `<` ��� `=`, �� �������� ������� ������ � ����. � ��������� ������ ����������� ������ �� ������ ����� � ������.
3) �������� ��������� ������ �� ����� � ������� ����� ������ �������. ���� ��������� `>`, �� ����������� ������ �� ������ ����� � ������ � ��������� ��� 3.
4) ������ �� ��������������� ������� � �������� ��� ��������� ����� ����� ������ �� ������. ���� ������� ������ ��� �� �����, �� ������� �� ��� 2.

���������: ***O(<nobr>*n*^2</nobr>)***

#### ����� ��������� � ��������� ���� �������:
��� ������ ����� ���������� `Lexer`, ������� ������������ ������� ������ � �������� �����.


��� ���������� ������ AST ����� �������������� __����� ������������ ������__, ������ ��� ������ ����� �� ������ �������� ������� ���������� ����������� ������������, � ������� �������� AST, �� � ����� ������������ ��������� ���������.
#### ������� ������� � �������� ������
##### ������� ������: 
���� � ���������� �������� ����� ��������� �� ����� �++.
##### �������� ������:
���� � AST �� ��������� ����.

##### ������:
������� ����:
```cpp 
int main(){
	int a = 5;
    std::cout << a;
}
```
�������� ����:
```
(Pr) -> (func: main) -> (type: int)
	          	     -> (body) -> (decl: a) -> (type: int)
			                     		    -> (value: 5)
		                       -> (op: <<) -> (stream: std::cout)
										   -> (value: a)
```