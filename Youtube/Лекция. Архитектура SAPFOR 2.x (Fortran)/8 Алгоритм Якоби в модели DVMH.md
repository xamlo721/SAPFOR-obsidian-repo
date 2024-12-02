```fortran
		REAL  A(L,L), B(L,L)
!IDVM$  DISTRIBUTE (BLOCK, BLOCK) :: A
!IDVM$  ALIGN B(IJ) WITH A(IJ)
		PRINT*, '********** TEST_JACOBI **********'
		DO IT = 1, ITMAX
!DVM$   REGION
!DVM$   PARALLEL (J,!) ON A(I, J)
			DO J = 2,L-1
				DO | = 2,L-1
					A(l, J) = B(I, J)
				ENDDO
			ENDDO
!DVM$   PARALLEL (J,I) ON B(I, J), SHADOW_RENEW(A)
			DO J=2, L-1
				DO 1=2, L-1
					B(I, J) = (A(I-1, J) +A(I, J-1)+ A(I#1, J) +A(I, J#1))/4
				ENDDO
			ENDDO
!DVM$ END REGION Anroputm Ako6u
		ENDDO
!DVM$ GET_ACTUAL(B) 
	PRINT *,B
	END eee
```