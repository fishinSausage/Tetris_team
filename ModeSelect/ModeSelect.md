# ��� ����â �ڵ� ����

2024.05.01 ��ȣ��

<br/>
<br/>
<br/>
��� : ���� ��带 ������ �� �ִ� ��� ����â�� ����  
�̿� ��� : ��� ���� - ȭ��ǥŰ ���Ʒ�, ��� Ȯ�� - �����̽���

## ��ü���� �ڵ� ���� 

���� �Լ��� title()�Լ��� ����� �� ��� ����â���μ��� title2()�� �����Ѵ�. 

���� ������ �Լ��� �����Ѵ�.
ȭ���� Ŭ�����Ѵ�. 
�׸��� Ű �Է� Ȯ��, ȭ�� ����� �ݺ��ϴ� for���� �����Ѵ�. 

Ű �Է��� �̹� �ִ� �ڵ�� ����ϰ� ����Ͽ���.
ȭ�� ��¿��� ����� �ֱ� ���� for���� cnt(count)������ ����Ͽ� 0.3�ʸ��� �ٲ�� �ߴ�. 

## �ڵ� �м�

```C
void title2(void)
{
    // reset
    void gop(int px, int py, char* txt); // �ڵ带 �ܼ�ȭ�ϱ� ���� �Լ�
    int x = 5, y = 4; // ������ ��ġ
    int mode = 0, mode_temp = -1; // ��� ����, ���� ��带 ����ϴ� ����
    int game_start = 0;
    system("cls"); // ȭ�� �ʱ�ȭ
    gop(x+10-5, y+0, ":: Select the mode ::");


    int cnt;
    for (cnt = 0;; cnt++) {
        // key_input
        if (_kbhit())
        {
            do { key = _getch(); } while (key == 224);
            switch (key) {
            case UP:
                if(mode>0) mode += -1;
                break;
            case DOWN:
                if(mode<1) mode += 1;
                break;
            case SPACE:
                game_start = 1;
                break;
            }
        }
        if(game_start) break; // ���� ����(��� ����â �Լ� ����)

		// ��尡 �ٲ� ������ ȭ�� �ʱ�ȭ
        if(mode_temp != mode) {
            gop(x+10-4, y+4, "    mode0    ");
            gop(x+10-4, y+6, "    mode1    ");
            mode_temp = mode;
			cnt = 0;
        }

        if(cnt % 60 == 0) // 0.6�� ��ⷯ �������� 0���� ��
        {
            gotoxy(x+10-4, y+4+2*mode); 
            printf(">>  mode%d  <<", mode); 
        }
        if(cnt % 60 == 30) // 0.6�� ��ⷯ �������� 0.3���� ��
        {
            gotoxy(x+10-4, y+4+2*mode);
            printf(" >> mode%d << ", mode); 
        }

        Sleep(10); // 0.1�� ������ 
    }
}

void gop(int px, int py, char* txt)
{
    gotoxy(px, py);
    printf("%s", txt);
}
```

## �ڵ带 �����ϴ� ��

���� �ڵ��� ��ܿ� title2�Լ��� ������ �ϰ� main�Լ����� title()�ٷ� �Ʒ��� title2()�� �Է��ϸ� �ȴ�. 

ex) main�Լ��� new �κ��� ���� �ȴ�. 

```C
void title2(void);
```

```C
int main() {
    int i;

    srand((unsigned)time(NULL)); //����ǥ���� 
    setcursortype(NOCURSOR); //Ŀ�� ���� 
    title(); //����Ÿ��Ʋ ȣ�� 
	// ---------------new----------------
    title2(); // ��� ����â ����
	// ----------------------------------

    reset(); //������ ���� 

    while (1) {
        for (i = 0; i < 5; i++) { //����� ��ĭ�������µ��� 5�� Ű�Է¹��� �� ���� 
            check_key(); //Ű�Է�Ȯ�� 
            draw_main(); //ȭ���� �׸� 
            Sleep(speed); //���Ӽӵ����� 
            if (crush_on && check_crush(bx, by + 1, b_rotation) == false) Sleep(100);
            //����� �浹���ΰ�� �߰��� �̵��� ȸ���� �ð��� ���� 
            if (space_key_on == 1) { //�����̽��ٸ� �������(hard drop) �߰��� �̵��� ȸ���Ҽ� ���� break; 
                space_key_on = 0;
                break;
            }
        }
        drop_block(); // ����� ��ĭ ���� 
        check_level_up(); // �������� üũ 
        check_game_over(); //���ӿ����� üũ 
        if (new_block_on == 1) new_block(); // �� �� flag�� �ִ� ��� ���ο� �� ���� 
    }
}
```