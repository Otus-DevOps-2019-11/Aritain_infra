# Aritain_infra
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

Aritain Infra repository

������ �� ��������-���� � GCP �������������� ��� ������ �������
ssh -t -i ~/.ssh/Ganhart -A Ganhart@*������� IP-����� bastion* ssh *���������� IP-����� ��������-�����*

��� �������� ��� ������ ��������������� ����� � ������� ssh
ssh someinternalhost

������ SSH �������� ��������� �������:
host bastion
        User Ganhart
        HostName 35.210.214.67
        Port 22
        IdentityFile ~/.ssh/Ganhart
        ForwardAgent yes

host someinternalhost
        User Ganhart
        hostname 10.132.0.4
        Port 22
        ProxyJump bastion

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

������ �������� ����:
----------
�������� SSH ���� ��� �������� � GCP

eval $(ssh-agent)
ssh-add ~/.ssh/Ganhart
ssh-add -L - ��������
----------
