Lab №5. Analysis of array sorts
--------------------
***
#### Task:
![The task](https://i.imgur.com/eXOAOt1.png)

>The program analyzes the sorting data

**Language**: Delphi

**Algorithm scheme**: 

In progress

**Code:**
``` pascal
program lab5;

{$APPTYPE CONSOLE}
const N=2000; MaxValue = 100; Shift = 50;
type TArray = array[1..N] of integer;
var BA,SA, MainArr: TArray;
    i,p,k: integer;
    ShellComparisons, ShellPermutations: integer;
    BubbleComparisons, BubblePermutations: integer;

procedure writeTableHead;
begin
  Writeln('+---------+-------------------------------+-------------------------------+');
  Writeln('|         |        Shell Sorting #1       |     Adv. Bubble Sorting #2    |');
  Writeln('|  Array  +---------------+---------------+---------------+---------------+');
  Writeln('|  type   |  Number of    |   Number of   |  Number of    |   Number of   |');
  Writeln('|         |  comparisons  |   exchanges   |  comparisons  |   exchanges   |');
  Writeln('+---------+---------------+---------------+---------------+---------------+');
end;
procedure coppy(var Arr, InitArr : TArray; Size: integer);
var i: integer;
begin
  for i:= 1 to Size do
    Arr[i] := InitArr[i];
end;

procedure ShellSort(var Size, Comp, Perm: integer);
var t,k,i,j,tmp,m:integer;
begin
  Comp:= 0;
  Perm:= 0;
  t := Trunc(Ln(Size) / Ln(2)) - 1;
  //writeln('t = ', t);
  for i:=1 to t do
  begin
    k:= (1 shl (t+1-i)) - 1;
    for j:=(k + 1) to Size do
    begin
      tmp:=SA[j];
      m:=j-k;
      While((m>=1) and (SA[m] > tmp)) do
      begin
        SA[M+k] := SA[m];
        m:=m-k;
        Inc(Comp);
        Inc(Perm);
      end;
      SA[m+k] := tmp;
      Inc(Perm);
      Inc(Comp);
    end;
  end;
end;

procedure Swap(var arr: TArray; var el1, el2: Integer);
var tmp:integer;
begin
  tmp:=arr[el1];
  arr[el1]:=arr[el2];
  arr[el2]:=tmp;
end;

procedure advBubble(var Size, Comp, Perm: Integer);
var i,k,z:integer;
F: Boolean;
begin
  Comp:= 0;
  Perm:= 0;
  for i:=1 to size do
  begin
    if(BA[i] > BA[i+1]) then
    begin
      z:=i+1;
      Swap(BA, i, z);
      Inc(Perm);
      k:=i;
      f:=True;
      while((k>1) and F) do
      begin
        if(BA[k-1] > BA[k]) then
        begin
          z:=k-1;
          Swap(BA, z,k);
          Inc(Perm);
          Dec(k);
        end
        else
          F:=False;
        Inc(Comp);
      end;
    end;
    Inc(Comp);
  end;
end;

procedure CreateTableRow(const k:integer; rtype:string; var SC, SP, BC, BP: Integer);
begin
  Writeln('|',k:4,' el. |', '':15,'|', '':15,'|', '':15,'|', '':15,'|');
  Writeln('|',rtype:9,'|',SC:10,'':5, '|',SP:10,'':5, '|',BC:10,'':5, '|',BP:10,'':5, '|');
  Writeln('+---------+---------------+---------------+---------------+---------------+');
end;

procedure reverse(var arr: TArray; const size: integer);
var i,tmp:Integer;
begin
  for i:=1 to size div 2 do
  begin
    tmp:=Arr[i];
    arr[i]:=Arr[k-i+1];
    Arr[k-i+1]:=tmp;
  end;
end;

begin
  Randomize;
  for i:=1 to N do
    MainArr[i] := Random(MaxValue) - Shift;
  writeTableHead;
  for p:=1 to 3 do
  begin
    case p of
      1 : k := 10;
      2 : k := 100;
      3 : k := 2000;
    end;
    coppy(SA,MainArr,k);
    coppy(BA,MainArr,k);

    // UNSORTED BEGIN
    ShellSort(k,ShellComparisons,ShellPermutations);
    advBubble(k,BubbleComparisons,BubblePermutations);
    CreateTableRow(k, 'unsorted' , ShellComparisons,ShellPermutations,BubbleComparisons,BubblePermutations);
    // UNSORTED END

    // SORTED BEGIN
    ShellSort(k,ShellComparisons,ShellPermutations);
    advBubble(k,BubbleComparisons,BubblePermutations);
    CreateTableRow(k, 'sorted  ' , ShellComparisons,ShellPermutations,BubbleComparisons,BubblePermutations);
    // SORTED END

    // REVERS START
    reverse(SA,k);
    reverse(BA,k);
    ShellSort(k,ShellComparisons,ShellPermutations);
    advBubble(k,BubbleComparisons,BubblePermutations);
    CreateTableRow(k, 'rev. ord.' , ShellComparisons,ShellPermutations,BubbleComparisons,BubblePermutations);
    // REVERS END

  end;
  Readln;
end.



```

