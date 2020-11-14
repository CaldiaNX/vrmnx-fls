# VRM-NX�t�@�C���A�g�V�X�e��

## �T�v
�uVRM-NX�t�@�C���A�g�V�X�e���v�iVRM-NX File linkege System�j�́u[�S���͌^�V�~�����[�^�[NX](http://www.imagic.co.jp/hobby/products/vrmnx/ "�S���͌^�V�~�����[�^�[NX")�v�iVRM-NX�j�̃r�����[�I�u�W�F�N�g���O�����琧�䂷�邽�߂�Python�ŋL�q���ꂽ�V�X�e���ł��B  
�^�C�}�[�C�x���g(�����0.1�b��)�Ƀ��C�A�E�g�t�@�C���Ɠ��K�w�ɂ���uread�v�t�H���_���̃t�@�C����ǂݍ��݁A�e�L�X�g�ŋL�q����Ă��閽�߂�VRM-NX�̖��߂ɕϊ����Ď��s���܂��B

## ���p���@
���C�A�E�g�t�@�C���Ɠ����t�H���_�K�w�Ɂuvrmnxfls.py�v�t�@�C���Ɓuread�v�uread_end�v�t�H���_���������܂��B  

```
C:\VRM-NX�i���j
�� \read
�� \read_end
�� \send (�C��)�usendSettingFile�v�֐��o�͗p
�� vrmnxfls.py
�� VRM-NX���C�A�E�g
```

�Ώۃ��C�A�E�g�̃��C�A�E�g�X�N���v�g�Ɉȉ��́����e��ǋL���܂��B  
�C�ӊ֐��͕K�v�ɉ����ė��p���Ă��������B

```py
import vrmapi
# ���t�@�C���A�g�V�X�e�����C���|�[�g
import vrmnxfls

def vrmevent(obj,ev,param):
    if ev == 'init':
        # ���N������0.1�b�Ԋu�̃^�C�}�[�C�x���g��o�^
        obj.SetEventTimer(0.1)
        # (�C��)send�t�H���_�Ƀ|�C���g�ƕҐ������o��
        vrmnxfls.sendSettingFile()
        # (�C��)���C�A�E�g���̑S�Ґ��̓d�����ꊇ�ݒ�i0:OFF, 1:ON�j
        vrmnxfls.setPowerAll(0)
    elif ev == 'broadcast':
        dummy = 1
    elif ev == 'timer':
        # ���^�C�}�[�C�x���g�Ńt�H���_�������Ď�
        vrmnxfls.readFile()
    elif ev == 'time':
        dummy = 1
    elif ev == 'after':
        dummy = 1
    elif ev == 'frame':
        dummy = 1
    elif ev == 'keydown':
        dummy = 1
```

�t�@�C���ǂݍ��݂ɐ�������ƁA�r���[���[�N�����̃X�N���v�g���O�� `load vrmnxfls.py` �ƕ\������܂��B

## readFile�֐�
�e�L�X�g�t�@�C�����uread�v�t�H���_�ɂ����`readFile`�֐����t�@�C����ǂݍ��݁A���߂����s���܂��B  
�ǂݍ��܂ꂽ�t�@�C���́uread_end�v�t�H���_�Ɉړ�����܂��B

### �t�@�C����
�t�@�C�����͔N���������b�uyyyymmddhhmmssfff.txt�v�ł��B  
�ǂݍ��ݑΏۂ́u��.txt�v�Ō��o���܂��B  
�N���������b�̖����K����FIFO�i������o���j�����炷�邽�߂̃��[���ł��B

### ���߃t�@�C���\��
�t�@�C���̓_�u���N�I�[�e�[�V���������A���s�����A�^�u��؂��1�sShift-JIS�e�L�X�g�t�@�C���ł��B

#### 1. Object���ʎq

| ���ʎq | �I�u�W�F�N�g | ���O |
| ---- | ---- | ---- |
| T | VRMTrain | �Ґ� |
| P | VRMPoint | �|�C���g |
| A | VRMATS | �����Z���T�[ |
| B | VRMBell | ���� |
| C | VRMCamera | �n��J���� |
| R | VRMCar | ���q |
| X | VRMCrossing | ���؁A�z�[���h�A |
| E | VRMEmitter | �G�~�b�^�[ |
| L | VRMLayout | ���C�A�E�g |
| M | VRMMotionPath | ���[�V�����p�X |
| G | VRMSignal | �M�� |
| K | VRMSky | �X�J�C�h�[���A�V�� |
| I | VRMSprite | �X�v���C�g |
| S | VRMSystem | �V�X�e�� |
| U | VRMTurntable | �^�[���^�[�u�� |

#### 2. ObjectID(int)
���ł͒��ڎQ�Ƃ̂ݑΉ����Ă��邽�߁A������ID������ꍇ�̓G���[�ƂȂ�܂��B  
�f�[�^���ł̎w���A���݃`�F�b�N�𓱓�����\��ł��B

#### 3. ���ߊ֐�
VRM-NX�Œ�`����Ă���e�I�u�W�F�N�g�̖��ߕ�����ł��B  
�����񂪖����Ȃ��͖̂��߂���������܂��B

#### 4. ����
���ߊ֐��ɕK�v�Ȉ������L�ڂ��܂��B  
������1�ȏ�Ȃ��ꍇ�͖��߂���������܂��B  
���ł͕K��1�ȏ���������Ă��܂����A����͖��߃Z�b�g�ɉ����ėv�f�����`�F�b�N����\��ł��B

### �\���T���v��
��Ԃ̑��x��ς���i���ID10�̑��x������50�ōō����x��50���ɕς���j
```
T	10	AutoSpeedCTRL	50	0.5
```

��Ԃ̐i�s������ς���i0�̓_�~�[�ϐ��j
```
T	10	Turn	0
```

��Ԃ̓d����ς���i0:OFF, 1:ON�j
```
T	10	SetPower	0
```

�|�C���g��؂�ւ���i�|�C���gID11�̌�����1���ɂ���j
```
P	11	SetBranch	1
```

## sendSettingFile�֐�
�usend�v�t�H���_�������Ԃ�`sendSettingFile`�֐������s����ƃ��C�A�E�g�t�@�C������Ґ��Ɨ�Ԃ̈ꗗ���^�u��؂��Shift_JIS�e�L�X�g�t�@�C���Ƃ���`send\yyyymmddhhmmssffffff.txt`�֏o�͂��܂��B  
���̏��́u�l�b�g���[�N�R���g���[���[�v���̐ݒ���Ƃ��ė��p�\�ł��B  
������̃��X�g��ID���ŏo�͂��܂��B  
�o�͂ɐ��������`send�t�H���_�Ƀ��C�A�E�g���t�@�C�����o�͂��܂����B`�ƕ\�����܂��B

- ���C�A�E�g�t�@�C���̏���N�����A�J�����g�f�B���N�g�����o�^�ɂ��t�H���_�ǂݍ��݂Ɏ��s����ꍇ������܂��B���̏ꍇ��VRM-NX���ċN�����Ă��������B

### 1.�Ґ��ꗗ

| �� | ���e | �ڍ� |
| ---- | ---- | ---- |
| 1 | t(�Œ蕶��) | Object���ʎq |
| 2 | ObjectID | GetID() |
| 3 | ObjectNAME | GetNAME() |
| 4 | X���W(��) | GetPosition()[0] |
| 5 | Y���W(����) | GetPosition()[1] |
| 6 | Z���W(�c) | GetPosition()[2] |
| 7 | ���x(�d��0.0�`1.0) | GetVoltage() |

```
t	10	TRAIN_10	2028.6000053961689	6.0	1096.0780848595002	0.0
t	25	TRAIN_25	1297.874999999999	6.0	1400.0000223802317	0.0
t	54	TRAIN_54	1291.4000003714773	6.0	1163.484177169418	0.0
t	64	TRAIN_64	2028.6000027358723	6.0	1332.593930070314	0.0
```

### 2.�|�C���g�ꗗ

| �� | ���e | �ڍ� |
| ---- | ---- | ---- |
| 1 | p(�Œ蕶��) | Object���ʎq |
| 2 | ObjectID | GetID() |
| 3 | ObjectNAME | GetNAME() |
| 4 | X���W(��) | GetPosition()[0] |
| 5 | Y���W(����) | GetPosition()[1] |
| 6 | Z���W(�c) | GetPosition()[2] |
| 7 | ������(0,1) | GetBranch() |

```
p	675	B����wC�n���XL	2108.00009006219	0.0	411.48450518271034	0
p	676	C����wB�n���XL	2364.0000885889813	0.0	445.18758033766994	0
p	677	C����wB�n���XL	2108.000088588982	0.0	445.18756914755403	0
p	678	B����wC�n���XR	2364.0000900621894	0.0	411.4845163728262	0
```

## �z�肳��闘�p�V�[��
- �O���v���O�����̉^�]�Ղ⎩���^�]�V�X�e���Ƃ̘A�g
- DCC�R���g���[�����g�����}�X�R������iCOM�A�g�E���ߕϊ��j
- ���C�A�E�g���m�̘A�g�������^���I�����C���^�]��

## ����
- v1.4 2020/10/24 �Ґ��̓d���𐧌䂷��usetPower�v�usetPowerAll�v�ǉ�
- v1.3 2020/09/27 �A���_�[�o�[��؂�ɂ��|�C���g�ꊇ�ݒ�ɑΉ�
- v1.2 2020/09/23 ���C�A�E�g���o�́usendSettingFile�v�ǉ�
- v1.1 2020/09/14 �����]���uTurn�v���ߒǉ�
- v1.0 2019/12/29 ���J

## ����̎����\��
- �ΏۃI�u�W�F�N�g�E���߃Z�b�g�̊g�[
- �C�x���g�h���u���iSetEvent�`�j�̒ǉ�
- �G���[����
- VRM-NX������̏o�͑Ή�
