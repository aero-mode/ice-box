```python

from    sqlalchemy                  import  MetaData, CursorResult
from    sqlalchemy                  import  select, update, insert
from    sqlalchemy                  import  String, Integer, Boolean
from    sqlalchemy.orm              import  DeclarativeBase, Mapped, mapped_column
from sqlalchemy.ext.asyncio import create_async_engine, async_sessionmaker, AsyncAttrs
from    rich.progress               import  track
from    sqlalchemy.exc              import  IntegrityError
import  logs
from    typing                      import  List, Tuple
from    datetime                    import  datetime


class Internal_manager:

    class Base(AsyncAttrs, DeclarativeBase):
        pass

  
    class Cliets(Base):
        __tablename__   =   'Cliets'
        id      :   Mapped[int] =   mapped_column(primary_key=True, unique=True)
        vkid    :   Mapped[int] =   mapped_column(unique=True)

  
    async def init(self):
        self.log = logs.Manager('internal.db')
        self.engine = create_async_engine(
            "sqlite+aiosqlite:///internal.db",
            echo = False
        )
        
        self.session = async_sessionmaker(self.engine)    
        async with self.engine.begin() as conn:
            await conn.run_sync(self.Base.metadata.create_all)

  
    async def get_client(self, vkid: int):
        try:
            async with self.engine.connect() as conn:
                result = await conn.execute(select(self.Cliets).where(self.Cliets.vkid == vkid))
                return result
        except Exception as e:
            self.log.console.print_exception()
            self.log.error(e)


    async def get_clients(self):
        try:
            async with self.engine.connect() as conn:
                result = await conn.execute(select(self.Cliets))
                return result
        except Exception as e:
            self.log.console.print_exception()
            self.log.error(e)

```

